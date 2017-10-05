---
title: "Przenieść dane z bazy danych MongoDB przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z bazy danych MongoDB przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: ac4ff55c765a5b874b81714c3d0063a5b4765a05
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="a7655-103">Przenoszenie danych z bazy danych MongoDB przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="a7655-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="a7655-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalną bazą danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7655-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="a7655-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a7655-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="a7655-106">Można skopiować danych z magazynu danych bazy danych MongoDB lokalnymi żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-106">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="a7655-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="a7655-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a7655-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, z magazynu danych bazy danych MongoDB do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych do magazynu danych bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7655-108">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a7655-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a7655-109">Prerequisites</span></span>
<span data-ttu-id="a7655-110">Dla usługi fabryka danych Azure można było nawiązać połączenia z lokalną bazą danych MongoDB należy zainstalować następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="a7655-110">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="a7655-111">Obsługiwane wersje bazy danych MongoDB: 2.4, 2.6 3.0 i 3.2.</span><span class="sxs-lookup"><span data-stu-id="a7655-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="a7655-112">Brama zarządzania danymi na tym samym komputerze, który jest hostem bazy danych lub na osobnym komputerze w celu uniknięcia konkurowanie o zasoby z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-112">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="a7655-113">Brama zarządzania danymi to oprogramowanie, które łączy lokalnych źródeł danych do usługi w chmurze w sposób bezpieczny i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="a7655-113">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="a7655-114">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="a7655-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="a7655-115">Zobacz [przenoszenia danych z lokalnymi do chmury](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy danych potoku do przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="a7655-116">Po zainstalowaniu bramy, automatycznie instaluje sterownik Microsoft MongoDB ODBC używany do łączenia z bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7655-116">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a7655-117">Należy używać bramy do łączenia się bazy danych MongoDB, nawet jeśli jest obsługiwany na maszynach wirtualnych Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="a7655-117">You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="a7655-118">Jeśli próbujesz połączyć się z wystąpieniem bazy danych MongoDB hostowanych w chmurze, można także zainstalować wystąpienie bramy na maszynie wirtualnej IaaS.</span><span class="sxs-lookup"><span data-stu-id="a7655-118">If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a7655-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a7655-119">Getting started</span></span>
<span data-ttu-id="a7655-120">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych bazy danych MongoDB lokalnymi przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a7655-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="a7655-121">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="a7655-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a7655-122">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a7655-123">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="a7655-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a7655-124">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a7655-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a7655-125">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="a7655-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="a7655-126">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a7655-127">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a7655-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a7655-128">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a7655-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a7655-129">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a7655-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a7655-130">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a7655-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a7655-131">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do skopiowania danych na lokalnym magazynem danych MongoDB, zobacz [przykład JSON: kopiowanie danych z bazy danych MongoDB do obiektów Blob platformy Azure](#json-example-copy-data-from-mongodb-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="a7655-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a7655-132">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do bazy danych MongoDB źródła:</span><span class="sxs-lookup"><span data-stu-id="a7655-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a7655-133">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="a7655-133">Linked service properties</span></span>
<span data-ttu-id="a7655-134">Poniższa tabela zawiera opis elementów JSON specyficzne dla **OnPremisesMongoDB** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="a7655-134">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="a7655-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a7655-135">Property</span></span> | <span data-ttu-id="a7655-136">Opis</span><span class="sxs-lookup"><span data-stu-id="a7655-136">Description</span></span> | <span data-ttu-id="a7655-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a7655-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7655-138">type</span><span class="sxs-lookup"><span data-stu-id="a7655-138">type</span></span> |<span data-ttu-id="a7655-139">Właściwość type musi mieć ustawioną: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="a7655-139">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="a7655-140">Tak</span><span class="sxs-lookup"><span data-stu-id="a7655-140">Yes</span></span> |
| <span data-ttu-id="a7655-141">serwer</span><span class="sxs-lookup"><span data-stu-id="a7655-141">server</span></span> |<span data-ttu-id="a7655-142">Adres IP lub hosta nazwę serwera bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7655-142">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="a7655-143">Tak</span><span class="sxs-lookup"><span data-stu-id="a7655-143">Yes</span></span> |
| <span data-ttu-id="a7655-144">port</span><span class="sxs-lookup"><span data-stu-id="a7655-144">port</span></span> |<span data-ttu-id="a7655-145">Port TCP używany przez serwer bazy danych MongoDB do nasłuchiwania dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="a7655-145">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="a7655-146">Opcjonalne, wartość domyślna: 27017</span><span class="sxs-lookup"><span data-stu-id="a7655-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="a7655-147">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="a7655-147">authenticationType</span></span> |<span data-ttu-id="a7655-148">Podstawowy, lub anonimowe.</span><span class="sxs-lookup"><span data-stu-id="a7655-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="a7655-149">Tak</span><span class="sxs-lookup"><span data-stu-id="a7655-149">Yes</span></span> |
| <span data-ttu-id="a7655-150">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a7655-150">username</span></span> |<span data-ttu-id="a7655-151">Konto użytkownika do bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7655-151">User account to access MongoDB.</span></span> |<span data-ttu-id="a7655-152">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="a7655-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="a7655-153">hasło</span><span class="sxs-lookup"><span data-stu-id="a7655-153">password</span></span> |<span data-ttu-id="a7655-154">Hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a7655-154">Password for the user.</span></span> |<span data-ttu-id="a7655-155">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="a7655-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="a7655-156">authSource</span><span class="sxs-lookup"><span data-stu-id="a7655-156">authSource</span></span> |<span data-ttu-id="a7655-157">Nazwa bazy danych MongoDB, który ma być używany w celu sprawdzenia poświadczeń dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a7655-157">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="a7655-158">Opcjonalnie (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="a7655-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="a7655-159">domyślne: używa konta administratora i baza danych określona za pomocą właściwości databaseName.</span><span class="sxs-lookup"><span data-stu-id="a7655-159">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="a7655-160">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="a7655-160">databaseName</span></span> |<span data-ttu-id="a7655-161">Nazwa bazy danych MongoDB, które chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="a7655-161">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="a7655-162">Tak</span><span class="sxs-lookup"><span data-stu-id="a7655-162">Yes</span></span> |
| <span data-ttu-id="a7655-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a7655-163">gatewayName</span></span> |<span data-ttu-id="a7655-164">Nazwa bramy, która uzyskuje dostęp do magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-164">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="a7655-165">Tak</span><span class="sxs-lookup"><span data-stu-id="a7655-165">Yes</span></span> |
| <span data-ttu-id="a7655-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a7655-166">encryptedCredential</span></span> |<span data-ttu-id="a7655-167">Poświadczenie szyfrowane przez bramę.</span><span class="sxs-lookup"><span data-stu-id="a7655-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="a7655-168">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="a7655-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="a7655-169">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="a7655-169">Dataset properties</span></span>
<span data-ttu-id="a7655-170">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a7655-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a7655-171">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="a7655-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a7655-172">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-172">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a7655-173">TypeProperties sekcja dla zestawu danych typu **MongoDbCollection** ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="a7655-173">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="a7655-174">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a7655-174">Property</span></span> | <span data-ttu-id="a7655-175">Opis</span><span class="sxs-lookup"><span data-stu-id="a7655-175">Description</span></span> | <span data-ttu-id="a7655-176">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a7655-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7655-177">CollectionName</span><span class="sxs-lookup"><span data-stu-id="a7655-177">collectionName</span></span> |<span data-ttu-id="a7655-178">Nazwa kolekcji w bazie danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7655-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="a7655-179">Tak</span><span class="sxs-lookup"><span data-stu-id="a7655-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a7655-180">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="a7655-180">Copy activity properties</span></span>
<span data-ttu-id="a7655-181">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a7655-181">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a7655-182">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="a7655-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a7655-183">Właściwości dostępne w **typeProperties** sekcji działania z drugiej strony zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="a7655-183">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="a7655-184">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="a7655-184">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a7655-185">Jeśli źródło jest typu **MongoDbSource** w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="a7655-185">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a7655-186">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a7655-186">Property</span></span> | <span data-ttu-id="a7655-187">Opis</span><span class="sxs-lookup"><span data-stu-id="a7655-187">Description</span></span> | <span data-ttu-id="a7655-188">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="a7655-188">Allowed values</span></span> | <span data-ttu-id="a7655-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a7655-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a7655-190">query</span><span class="sxs-lookup"><span data-stu-id="a7655-190">query</span></span> |<span data-ttu-id="a7655-191">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-191">Use the custom query to read data.</span></span> |<span data-ttu-id="a7655-192">Ciąg zapytania SQL 92.</span><span class="sxs-lookup"><span data-stu-id="a7655-192">SQL-92 query string.</span></span> <span data-ttu-id="a7655-193">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="a7655-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="a7655-194">Nie (Jeśli **collectionName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="a7655-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="a7655-195">Przykład JSON: kopiowanie danych z bazy danych MongoDB do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a7655-195">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="a7655-196">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a7655-196">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a7655-197">Widoczny jest sposób skopiować dane z lokalnej bazy danych MongoDB do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a7655-197">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="a7655-198">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="a7655-198">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="a7655-199">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="a7655-199">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="a7655-200">Połączonej usługi typu [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a7655-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="a7655-201">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a7655-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a7655-202">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a7655-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="a7655-203">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a7655-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a7655-204">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [MongoDbSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a7655-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a7655-205">Przykład kopiuje dane z wyniku kwerendy w bazie danych MongoDB do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a7655-205">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="a7655-206">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="a7655-206">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a7655-207">Pierwszym krokiem instalacji bramy zarządzania danymi, zgodnie z instrukcjami wyświetlanymi w [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a7655-207">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="a7655-208">**Bazy danych MongoDB połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="a7655-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="a7655-209">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="a7655-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="a7655-210">**Wejściowy zestaw danych MongoDB:** ustawienie "external": "prawda" informuje usługi fabryka danych czy tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="a7655-210">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="a7655-211">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="a7655-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a7655-212">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="a7655-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a7655-213">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="a7655-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a7655-214">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="a7655-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="a7655-215">**Aktywność kopiowania w potoku z bazy danych MongoDB źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="a7655-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="a7655-216">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania powyższe dane wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a7655-216">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a7655-217">W definicji JSON potoku **źródła** ustawiono typ **MongoDbSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a7655-217">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a7655-218">Określony dla zapytania SQL **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="a7655-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="a7655-219">Schemat fabryka danych</span><span class="sxs-lookup"><span data-stu-id="a7655-219">Schema by Data Factory</span></span>
<span data-ttu-id="a7655-220">Usługi fabryka danych Azure wnioskuje schemat z kolekcji bazy danych MongoDB przy użyciu najnowszych 100 dokumentów w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="a7655-220">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="a7655-221">Jeśli te dokumenty 100 nie zawierają pełny schemat, niektóre kolumny można zignorować podczas operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a7655-221">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="a7655-222">Mapowanie typu dla bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="a7655-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="a7655-223">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, wykonuje działanie kopiowania automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="a7655-223">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="a7655-224">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="a7655-224">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a7655-225">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="a7655-225">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a7655-226">Podczas przenoszenia danych do bazy danych MongoDB z bazy danych MongoDB typy są używane następujące mapowania do typów .NET.</span><span class="sxs-lookup"><span data-stu-id="a7655-226">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="a7655-227">Typ bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="a7655-227">MongoDB type</span></span> | <span data-ttu-id="a7655-228">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="a7655-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="a7655-229">Binarne</span><span class="sxs-lookup"><span data-stu-id="a7655-229">Binary</span></span> |<span data-ttu-id="a7655-230">Byte]</span><span class="sxs-lookup"><span data-stu-id="a7655-230">Byte[]</span></span> |
| <span data-ttu-id="a7655-231">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a7655-231">Boolean</span></span> |<span data-ttu-id="a7655-232">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a7655-232">Boolean</span></span> |
| <span data-ttu-id="a7655-233">Date</span><span class="sxs-lookup"><span data-stu-id="a7655-233">Date</span></span> |<span data-ttu-id="a7655-234">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="a7655-234">DateTime</span></span> |
| <span data-ttu-id="a7655-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="a7655-235">NumberDouble</span></span> |<span data-ttu-id="a7655-236">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="a7655-236">Double</span></span> |
| <span data-ttu-id="a7655-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="a7655-237">NumberInt</span></span> |<span data-ttu-id="a7655-238">Int32</span><span class="sxs-lookup"><span data-stu-id="a7655-238">Int32</span></span> |
| <span data-ttu-id="a7655-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="a7655-239">NumberLong</span></span> |<span data-ttu-id="a7655-240">Int64</span><span class="sxs-lookup"><span data-stu-id="a7655-240">Int64</span></span> |
| <span data-ttu-id="a7655-241">Identyfikator obiektu</span><span class="sxs-lookup"><span data-stu-id="a7655-241">ObjectID</span></span> |<span data-ttu-id="a7655-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a7655-242">String</span></span> |
| <span data-ttu-id="a7655-243">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a7655-243">String</span></span> |<span data-ttu-id="a7655-244">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a7655-244">String</span></span> |
| <span data-ttu-id="a7655-245">IDENTYFIKATOR UUID</span><span class="sxs-lookup"><span data-stu-id="a7655-245">UUID</span></span> |<span data-ttu-id="a7655-246">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="a7655-246">Guid</span></span> |
| <span data-ttu-id="a7655-247">Obiekt</span><span class="sxs-lookup"><span data-stu-id="a7655-247">Object</span></span> |<span data-ttu-id="a7655-248">Renormalized do spłaszczenia kolumn z "_" jako separatora zagnieżdżonych</span><span class="sxs-lookup"><span data-stu-id="a7655-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="a7655-249">Aby dowiedzieć się więcej o obsługę tablic za pomocą tabele wirtualne, zapoznaj się [obsługę złożonych typów przy użyciu tabele wirtualne](#support-for-complex-types-using-virtual-tables) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a7655-249">To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="a7655-250">Obecnie nie są obsługiwane następujące typy danych MongoDB: DBPointer, JavaScript, maksymalna liczba na minutę klucza, wyrażenie regularne, Symbol, Timestamp, niezdefiniowane</span><span class="sxs-lookup"><span data-stu-id="a7655-250">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="a7655-251">Obsługę złożonych typów przy użyciu tabele wirtualne</span><span class="sxs-lookup"><span data-stu-id="a7655-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="a7655-252">Fabryka danych Azure używa wbudowanego sterownika ODBC do nawiązania połączenia, a następnie skopiować dane z bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7655-252">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="a7655-253">Typów złożonych takich jak macierze lub obiektów z różnymi typami wszystkich dokumentów sterownik ponownie normalizuje danych do odpowiednich tabel wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="a7655-253">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="a7655-254">W szczególności jeśli tabela zawiera takich kolumn, sterownik generuje następujące tabele wirtualne:</span><span class="sxs-lookup"><span data-stu-id="a7655-254">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="a7655-255">A **tabeli podstawowej**, który zawiera te same dane jako prawdziwe tabeli z wyjątkiem kolumny typu złożonego.</span><span class="sxs-lookup"><span data-stu-id="a7655-255">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="a7655-256">Tabela podstawowa używa tej samej nazwie jako prawdziwe tabeli, która reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="a7655-256">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="a7655-257">A **tabeli wirtualnej** dla każdej kolumny typu złożonego, która rozszerza zagnieżdżone dane.</span><span class="sxs-lookup"><span data-stu-id="a7655-257">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="a7655-258">Tabele wirtualne są nazywane przy użyciu nazwy tabeli prawdziwe, separator "_" i nazwę tablicy lub obiektu.</span><span class="sxs-lookup"><span data-stu-id="a7655-258">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="a7655-259">Tabele wirtualne odwołują się do danych w tabeli prawdziwe, włączanie dostępu do danych nieznormalizowany sterownika.</span><span class="sxs-lookup"><span data-stu-id="a7655-259">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="a7655-260">Zobacz przykład sekcję poniżej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a7655-260">See Example section below details.</span></span> <span data-ttu-id="a7655-261">Ma dostęp do zawartości tablic bazy danych MongoDB, zapytań i przyłączanie tabel wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="a7655-261">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="a7655-262">Można użyć [kreatora kopiowania](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) intuicyjnie wyświetlić listę tabel w bazie danych MongoDB, łącznie z tabelami wirtualnego i przeglądać dane wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="a7655-262">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="a7655-263">Można również utworzyć zapytanie w kreatorze kopiowania i weryfikacji, aby zobaczyć wynik.</span><span class="sxs-lookup"><span data-stu-id="a7655-263">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="a7655-264">Przykład</span><span class="sxs-lookup"><span data-stu-id="a7655-264">Example</span></span>
<span data-ttu-id="a7655-265">Na przykład "ExampleTable" poniżej znajduje się tabela bazy danych MongoDB o jedną kolumnę z tablicę obiektów w każdej komórce — faktury i jedną kolumnę z tablicą typów skalarnych — klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="a7655-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="a7655-266">_id</span><span class="sxs-lookup"><span data-stu-id="a7655-266">_id</span></span> | <span data-ttu-id="a7655-267">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="a7655-267">Customer Name</span></span> | <span data-ttu-id="a7655-268">Faktury</span><span class="sxs-lookup"><span data-stu-id="a7655-268">Invoices</span></span> | <span data-ttu-id="a7655-269">Poziom usług</span><span class="sxs-lookup"><span data-stu-id="a7655-269">Service Level</span></span> | <span data-ttu-id="a7655-270">Klasyfikacje</span><span class="sxs-lookup"><span data-stu-id="a7655-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a7655-271">1111</span><span class="sxs-lookup"><span data-stu-id="a7655-271">1111</span></span> |<span data-ttu-id="a7655-272">ABC</span><span class="sxs-lookup"><span data-stu-id="a7655-272">ABC</span></span> |<span data-ttu-id="a7655-273">[{invoice_id: elementu "123",: "tostera", cena: Rabat "456",: "0,2"}, {invoice_id: "124", element: "piec", cena: Zniżka "1235": "0,2"}]</span><span class="sxs-lookup"><span data-stu-id="a7655-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="a7655-274">Srebrny</span><span class="sxs-lookup"><span data-stu-id="a7655-274">Silver</span></span> |<span data-ttu-id="a7655-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="a7655-275">[5,6]</span></span> |
| <span data-ttu-id="a7655-276">2222</span><span class="sxs-lookup"><span data-stu-id="a7655-276">2222</span></span> |<span data-ttu-id="a7655-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="a7655-277">XYZ</span></span> |<span data-ttu-id="a7655-278">[{invoice_id: element "135": "lodówko", cena: Rabat "12543": "0,0"}]</span><span class="sxs-lookup"><span data-stu-id="a7655-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="a7655-279">Gold</span><span class="sxs-lookup"><span data-stu-id="a7655-279">Gold</span></span> |<span data-ttu-id="a7655-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="a7655-280">[1,2]</span></span> |

<span data-ttu-id="a7655-281">Sterownik przetwarzający generuje wiele tabel wirtualnego do reprezentowania tej pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="a7655-281">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="a7655-282">Pierwszy tabeli wirtualnej jest tabela podstawowa o nazwie "ExampleTable", pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a7655-282">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="a7655-283">Podstawowa tabela zawiera wszystkie dane z oryginalnej tabeli, ale dane z macierzami została pominięta i jest rozwinięta w tabelach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a7655-283">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="a7655-284">_id</span><span class="sxs-lookup"><span data-stu-id="a7655-284">_id</span></span> | <span data-ttu-id="a7655-285">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="a7655-285">Customer Name</span></span> | <span data-ttu-id="a7655-286">Poziom usług</span><span class="sxs-lookup"><span data-stu-id="a7655-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7655-287">1111</span><span class="sxs-lookup"><span data-stu-id="a7655-287">1111</span></span> |<span data-ttu-id="a7655-288">ABC</span><span class="sxs-lookup"><span data-stu-id="a7655-288">ABC</span></span> |<span data-ttu-id="a7655-289">Srebrny</span><span class="sxs-lookup"><span data-stu-id="a7655-289">Silver</span></span> |
| <span data-ttu-id="a7655-290">2222</span><span class="sxs-lookup"><span data-stu-id="a7655-290">2222</span></span> |<span data-ttu-id="a7655-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="a7655-291">XYZ</span></span> |<span data-ttu-id="a7655-292">Gold</span><span class="sxs-lookup"><span data-stu-id="a7655-292">Gold</span></span> |

<span data-ttu-id="a7655-293">W poniższych tabelach przedstawiono wirtualnego tabel, które reprezentują oryginalnego tablic w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a7655-293">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="a7655-294">Te tabele zawierać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="a7655-294">These tables contain the following:</span></span>

* <span data-ttu-id="a7655-295">Odwołanie do oryginalnego kolumna klucza podstawowego odpowiadający wiersza oryginalnej tablicy (za pomocą kolumny _id)</span><span class="sxs-lookup"><span data-stu-id="a7655-295">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="a7655-296">Wskazanie pozycji danych w oryginalnej tablicy</span><span class="sxs-lookup"><span data-stu-id="a7655-296">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="a7655-297">Rozwinięte danych dla każdego elementu w tablicy</span><span class="sxs-lookup"><span data-stu-id="a7655-297">The expanded data for each element within the array</span></span>

<span data-ttu-id="a7655-298">Tabela "ExampleTable_Invoices":</span><span class="sxs-lookup"><span data-stu-id="a7655-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="a7655-299">_id</span><span class="sxs-lookup"><span data-stu-id="a7655-299">_id</span></span> | <span data-ttu-id="a7655-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="a7655-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="a7655-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="a7655-301">invoice_id</span></span> | <span data-ttu-id="a7655-302">Element</span><span class="sxs-lookup"><span data-stu-id="a7655-302">item</span></span> | <span data-ttu-id="a7655-303">price</span><span class="sxs-lookup"><span data-stu-id="a7655-303">price</span></span> | <span data-ttu-id="a7655-304">Rabat</span><span class="sxs-lookup"><span data-stu-id="a7655-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a7655-305">1111</span><span class="sxs-lookup"><span data-stu-id="a7655-305">1111</span></span> |<span data-ttu-id="a7655-306">0</span><span class="sxs-lookup"><span data-stu-id="a7655-306">0</span></span> |<span data-ttu-id="a7655-307">123</span><span class="sxs-lookup"><span data-stu-id="a7655-307">123</span></span> |<span data-ttu-id="a7655-308">tostera</span><span class="sxs-lookup"><span data-stu-id="a7655-308">toaster</span></span> |<span data-ttu-id="a7655-309">456</span><span class="sxs-lookup"><span data-stu-id="a7655-309">456</span></span> |<span data-ttu-id="a7655-310">0.2</span><span class="sxs-lookup"><span data-stu-id="a7655-310">0.2</span></span> |
| <span data-ttu-id="a7655-311">1111</span><span class="sxs-lookup"><span data-stu-id="a7655-311">1111</span></span> |<span data-ttu-id="a7655-312">1</span><span class="sxs-lookup"><span data-stu-id="a7655-312">1</span></span> |<span data-ttu-id="a7655-313">124</span><span class="sxs-lookup"><span data-stu-id="a7655-313">124</span></span> |<span data-ttu-id="a7655-314">Piec</span><span class="sxs-lookup"><span data-stu-id="a7655-314">oven</span></span> |<span data-ttu-id="a7655-315">1235</span><span class="sxs-lookup"><span data-stu-id="a7655-315">1235</span></span> |<span data-ttu-id="a7655-316">0.2</span><span class="sxs-lookup"><span data-stu-id="a7655-316">0.2</span></span> |
| <span data-ttu-id="a7655-317">2222</span><span class="sxs-lookup"><span data-stu-id="a7655-317">2222</span></span> |<span data-ttu-id="a7655-318">0</span><span class="sxs-lookup"><span data-stu-id="a7655-318">0</span></span> |<span data-ttu-id="a7655-319">135</span><span class="sxs-lookup"><span data-stu-id="a7655-319">135</span></span> |<span data-ttu-id="a7655-320">lodówko</span><span class="sxs-lookup"><span data-stu-id="a7655-320">fridge</span></span> |<span data-ttu-id="a7655-321">12543</span><span class="sxs-lookup"><span data-stu-id="a7655-321">12543</span></span> |<span data-ttu-id="a7655-322">0.0</span><span class="sxs-lookup"><span data-stu-id="a7655-322">0.0</span></span> |

<span data-ttu-id="a7655-323">Tabela "ExampleTable_Ratings":</span><span class="sxs-lookup"><span data-stu-id="a7655-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="a7655-324">_id</span><span class="sxs-lookup"><span data-stu-id="a7655-324">_id</span></span> | <span data-ttu-id="a7655-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="a7655-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="a7655-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="a7655-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7655-327">1111</span><span class="sxs-lookup"><span data-stu-id="a7655-327">1111</span></span> |<span data-ttu-id="a7655-328">0</span><span class="sxs-lookup"><span data-stu-id="a7655-328">0</span></span> |<span data-ttu-id="a7655-329">5</span><span class="sxs-lookup"><span data-stu-id="a7655-329">5</span></span> |
| <span data-ttu-id="a7655-330">1111</span><span class="sxs-lookup"><span data-stu-id="a7655-330">1111</span></span> |<span data-ttu-id="a7655-331">1</span><span class="sxs-lookup"><span data-stu-id="a7655-331">1</span></span> |<span data-ttu-id="a7655-332">6</span><span class="sxs-lookup"><span data-stu-id="a7655-332">6</span></span> |
| <span data-ttu-id="a7655-333">2222</span><span class="sxs-lookup"><span data-stu-id="a7655-333">2222</span></span> |<span data-ttu-id="a7655-334">0</span><span class="sxs-lookup"><span data-stu-id="a7655-334">0</span></span> |<span data-ttu-id="a7655-335">1</span><span class="sxs-lookup"><span data-stu-id="a7655-335">1</span></span> |
| <span data-ttu-id="a7655-336">2222</span><span class="sxs-lookup"><span data-stu-id="a7655-336">2222</span></span> |<span data-ttu-id="a7655-337">1</span><span class="sxs-lookup"><span data-stu-id="a7655-337">1</span></span> |<span data-ttu-id="a7655-338">2</span><span class="sxs-lookup"><span data-stu-id="a7655-338">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="a7655-339">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="a7655-339">Map source to sink columns</span></span>
<span data-ttu-id="a7655-340">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a7655-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a7655-341">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="a7655-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="a7655-342">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="a7655-342">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a7655-343">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="a7655-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a7655-344">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="a7655-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a7655-345">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="a7655-345">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a7655-346">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="a7655-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a7655-347">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="a7655-347">Performance and Tuning</span></span>
<span data-ttu-id="a7655-348">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="a7655-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7655-349">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7655-349">Next Steps</span></span>
<span data-ttu-id="a7655-350">Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykuł instrukcje krok po kroku dla tworzenie potoku danych, które przenosi dane z lokalnego magazynu danych do magazynu danych Azure.</span><span class="sxs-lookup"><span data-stu-id="a7655-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
