---
title: "aaaMove dane z bazy danych MongoDB przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove dane z bazy danych MongoDB bazy danych przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="019ff-103">Przenoszenie danych z bazy danych MongoDB przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="019ff-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="019ff-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="019ff-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="019ff-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="019ff-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="019ff-106">Możesz skopiować dane z lokalnej bazy danych MongoDB magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="019ff-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="019ff-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="019ff-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="019ff-108">Fabryka danych aktualnie obsługuje tylko przeniesienie tooother magazyny danych magazynu danych z danych MongoDB, ale nie do przenoszenia danych z magazynu danych innych danych magazynów tooan bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="019ff-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="019ff-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="019ff-109">Prerequisites</span></span>
<span data-ttu-id="019ff-110">Hello fabryki danych Azure toobe stanie tooconnect tooyour lokalnej bazy danych MongoDB bazy danych usługi należy zainstalować hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="019ff-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="019ff-111">Obsługiwane wersje bazy danych MongoDB: 2.4, 2.6 3.0 i 3.2.</span><span class="sxs-lookup"><span data-stu-id="019ff-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="019ff-112">Brama zarządzania danymi na hello tej samej maszynie tej bazy danych hello hostów lub na tooavoid osobnym komputerze fizycznym, konkurowanie o zasoby z hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="019ff-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="019ff-113">Brama zarządzania danymi to oprogramowanie, które nawiązuje połączenie usługi toocloud źródeł danych lokalnych w sposób bezpieczny i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="019ff-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="019ff-114">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="019ff-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="019ff-115">Zobacz [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy hello toomove potoku danych.</span><span class="sxs-lookup"><span data-stu-id="019ff-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="019ff-116">Po zainstalowaniu bramy hello automatycznie instaluje tooMongoDB tooconnect sterownik Microsoft MongoDB ODBC.</span><span class="sxs-lookup"><span data-stu-id="019ff-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="019ff-117">Należy toouse hello bramy tooconnect tooMongoDB, nawet jeśli jest obsługiwany na maszynach wirtualnych Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="019ff-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="019ff-118">Jeśli próbujesz tooconnect tooan wystąpienie bazy danych MongoDB hostowanych w chmurze, można także zainstalować wystąpienie bramy hello w hello maszyn wirtualnych IaaS.</span><span class="sxs-lookup"><span data-stu-id="019ff-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="019ff-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="019ff-119">Getting started</span></span>
<span data-ttu-id="019ff-120">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych bazy danych MongoDB lokalnymi przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="019ff-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="019ff-121">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="019ff-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="019ff-122">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="019ff-123">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="019ff-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="019ff-124">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="019ff-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="019ff-125">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="019ff-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="019ff-126">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="019ff-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="019ff-127">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="019ff-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="019ff-128">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="019ff-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="019ff-129">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="019ff-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="019ff-130">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="019ff-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="019ff-131">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych bazy danych MongoDB lokalnych, zobacz [przykład JSON: kopiowanie danych z bazy danych MongoDB tooAzure obiektu Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="019ff-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="019ff-132">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek tooMongoDB określonego źródła:</span><span class="sxs-lookup"><span data-stu-id="019ff-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="019ff-133">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="019ff-133">Linked service properties</span></span>
<span data-ttu-id="019ff-134">Witaj Poniższa tabela zawiera opis elementów JSON określonych zbyt**OnPremisesMongoDB** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="019ff-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="019ff-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="019ff-135">Property</span></span> | <span data-ttu-id="019ff-136">Opis</span><span class="sxs-lookup"><span data-stu-id="019ff-136">Description</span></span> | <span data-ttu-id="019ff-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="019ff-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="019ff-138">type</span><span class="sxs-lookup"><span data-stu-id="019ff-138">type</span></span> |<span data-ttu-id="019ff-139">musi mieć ustawioną właściwość type Hello: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="019ff-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="019ff-140">Tak</span><span class="sxs-lookup"><span data-stu-id="019ff-140">Yes</span></span> |
| <span data-ttu-id="019ff-141">serwer</span><span class="sxs-lookup"><span data-stu-id="019ff-141">server</span></span> |<span data-ttu-id="019ff-142">Adres IP lub hosta nazwę serwera bazy danych MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="019ff-143">Tak</span><span class="sxs-lookup"><span data-stu-id="019ff-143">Yes</span></span> |
| <span data-ttu-id="019ff-144">port</span><span class="sxs-lookup"><span data-stu-id="019ff-144">port</span></span> |<span data-ttu-id="019ff-145">Port TCP, którego hello serwera bazy danych MongoDB używa toolisten dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="019ff-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="019ff-146">Opcjonalne, wartość domyślna: 27017</span><span class="sxs-lookup"><span data-stu-id="019ff-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="019ff-147">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="019ff-147">authenticationType</span></span> |<span data-ttu-id="019ff-148">Podstawowy, lub anonimowe.</span><span class="sxs-lookup"><span data-stu-id="019ff-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="019ff-149">Tak</span><span class="sxs-lookup"><span data-stu-id="019ff-149">Yes</span></span> |
| <span data-ttu-id="019ff-150">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="019ff-150">username</span></span> |<span data-ttu-id="019ff-151">Tooaccess konta użytkownika bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="019ff-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="019ff-152">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="019ff-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="019ff-153">hasło</span><span class="sxs-lookup"><span data-stu-id="019ff-153">password</span></span> |<span data-ttu-id="019ff-154">Hasło dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-154">Password for hello user.</span></span> |<span data-ttu-id="019ff-155">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="019ff-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="019ff-156">authSource</span><span class="sxs-lookup"><span data-stu-id="019ff-156">authSource</span></span> |<span data-ttu-id="019ff-157">Nazwa bazy danych MongoDB hello czy chcesz toouse toocheck swoje poświadczenia dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="019ff-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="019ff-158">Opcjonalnie (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="019ff-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="019ff-159">domyślne: używa konta administratora hello i hello bazy danych określona za pomocą właściwości databaseName.</span><span class="sxs-lookup"><span data-stu-id="019ff-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="019ff-160">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="019ff-160">databaseName</span></span> |<span data-ttu-id="019ff-161">Nazwa bazy danych MongoDB hello, które mają tooaccess.</span><span class="sxs-lookup"><span data-stu-id="019ff-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="019ff-162">Tak</span><span class="sxs-lookup"><span data-stu-id="019ff-162">Yes</span></span> |
| <span data-ttu-id="019ff-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="019ff-163">gatewayName</span></span> |<span data-ttu-id="019ff-164">Nazwa bramy hello, który uzyskuje dostęp do magazynu danych hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="019ff-165">Tak</span><span class="sxs-lookup"><span data-stu-id="019ff-165">Yes</span></span> |
| <span data-ttu-id="019ff-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="019ff-166">encryptedCredential</span></span> |<span data-ttu-id="019ff-167">Poświadczenie szyfrowane przez bramę.</span><span class="sxs-lookup"><span data-stu-id="019ff-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="019ff-168">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="019ff-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="019ff-169">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="019ff-169">Dataset properties</span></span>
<span data-ttu-id="019ff-170">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="019ff-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="019ff-171">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="019ff-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="019ff-172">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="019ff-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="019ff-173">Witaj typeProperties sekcja dla zestawu danych typu **MongoDbCollection** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="019ff-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="019ff-174">Właściwość</span><span class="sxs-lookup"><span data-stu-id="019ff-174">Property</span></span> | <span data-ttu-id="019ff-175">Opis</span><span class="sxs-lookup"><span data-stu-id="019ff-175">Description</span></span> | <span data-ttu-id="019ff-176">Wymagane</span><span class="sxs-lookup"><span data-stu-id="019ff-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="019ff-177">CollectionName</span><span class="sxs-lookup"><span data-stu-id="019ff-177">collectionName</span></span> |<span data-ttu-id="019ff-178">Nazwa kolekcji hello w bazie danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="019ff-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="019ff-179">Tak</span><span class="sxs-lookup"><span data-stu-id="019ff-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="019ff-180">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="019ff-180">Copy activity properties</span></span>
<span data-ttu-id="019ff-181">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="019ff-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="019ff-182">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="019ff-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="019ff-183">Właściwości dostępne w hello **typeProperties** sekcji aktywności hello na powitania drugiej zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="019ff-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="019ff-184">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="019ff-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="019ff-185">Gdy źródło hello jest typu **MongoDbSource** hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="019ff-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="019ff-186">Właściwość</span><span class="sxs-lookup"><span data-stu-id="019ff-186">Property</span></span> | <span data-ttu-id="019ff-187">Opis</span><span class="sxs-lookup"><span data-stu-id="019ff-187">Description</span></span> | <span data-ttu-id="019ff-188">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="019ff-188">Allowed values</span></span> | <span data-ttu-id="019ff-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="019ff-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="019ff-190">query</span><span class="sxs-lookup"><span data-stu-id="019ff-190">query</span></span> |<span data-ttu-id="019ff-191">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="019ff-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="019ff-192">Ciąg zapytania SQL 92.</span><span class="sxs-lookup"><span data-stu-id="019ff-192">SQL-92 query string.</span></span> <span data-ttu-id="019ff-193">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="019ff-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="019ff-194">Nie (Jeśli **collectionName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="019ff-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="019ff-195">Przykład JSON: kopiowanie danych z bazy danych MongoDB tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="019ff-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="019ff-196">W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="019ff-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="019ff-197">Widoczny jest sposób toocopy dane z lokalnej bazy danych MongoDB tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="019ff-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="019ff-198">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="019ff-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="019ff-199">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="019ff-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="019ff-200">Połączonej usługi typu [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="019ff-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="019ff-201">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="019ff-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="019ff-202">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="019ff-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="019ff-203">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="019ff-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="019ff-204">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [MongoDbSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="019ff-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="019ff-205">przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa bazy danych MongoDB, co godzinę.</span><span class="sxs-lookup"><span data-stu-id="019ff-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="019ff-206">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="019ff-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="019ff-207">Pierwszym krokiem instalacji bramy zarządzania danymi hello zgodnie z instrukcjami hello hello [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="019ff-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="019ff-208">**Bazy danych MongoDB połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="019ff-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="019ff-209">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="019ff-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="019ff-210">**Wejściowy zestaw danych MongoDB:** ustawienie "external": "prawda" informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="019ff-211">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="019ff-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="019ff-212">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="019ff-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="019ff-213">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="019ff-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="019ff-214">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="019ff-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="019ff-215">**Aktywność kopiowania w potoku z bazy danych MongoDB źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="019ff-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="019ff-216">potok Hello zawiera działanie kopiowania, który hello toouse skonfigurowanych powyżej wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="019ff-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="019ff-217">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**MongoDbSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="019ff-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="019ff-218">Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="019ff-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


## <a name="schema-by-data-factory"></a><span data-ttu-id="019ff-219">Schemat fabryka danych</span><span class="sxs-lookup"><span data-stu-id="019ff-219">Schema by Data Factory</span></span>
<span data-ttu-id="019ff-220">Usługi fabryka danych Azure wnioskuje schemat z kolekcji bazy danych MongoDB przy użyciu hello najnowsze 100 dokumentów w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="019ff-221">Jeśli te dokumenty 100 nie zawierają pełny schemat, można zignorować podczas operacji kopiowania hello niektóre kolumny.</span><span class="sxs-lookup"><span data-stu-id="019ff-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="019ff-222">Mapowanie typu dla bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="019ff-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="019ff-223">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="019ff-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="019ff-224">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="019ff-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="019ff-225">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="019ff-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="019ff-226">Podczas przenoszenia danych tooMongoDB hello następującego mapowania są używane z typów too.NET typy bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="019ff-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="019ff-227">Typ bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="019ff-227">MongoDB type</span></span> | <span data-ttu-id="019ff-228">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="019ff-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="019ff-229">Binarne</span><span class="sxs-lookup"><span data-stu-id="019ff-229">Binary</span></span> |<span data-ttu-id="019ff-230">Byte]</span><span class="sxs-lookup"><span data-stu-id="019ff-230">Byte[]</span></span> |
| <span data-ttu-id="019ff-231">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="019ff-231">Boolean</span></span> |<span data-ttu-id="019ff-232">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="019ff-232">Boolean</span></span> |
| <span data-ttu-id="019ff-233">Date</span><span class="sxs-lookup"><span data-stu-id="019ff-233">Date</span></span> |<span data-ttu-id="019ff-234">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="019ff-234">DateTime</span></span> |
| <span data-ttu-id="019ff-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="019ff-235">NumberDouble</span></span> |<span data-ttu-id="019ff-236">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="019ff-236">Double</span></span> |
| <span data-ttu-id="019ff-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="019ff-237">NumberInt</span></span> |<span data-ttu-id="019ff-238">Int32</span><span class="sxs-lookup"><span data-stu-id="019ff-238">Int32</span></span> |
| <span data-ttu-id="019ff-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="019ff-239">NumberLong</span></span> |<span data-ttu-id="019ff-240">Int64</span><span class="sxs-lookup"><span data-stu-id="019ff-240">Int64</span></span> |
| <span data-ttu-id="019ff-241">Identyfikator obiektu</span><span class="sxs-lookup"><span data-stu-id="019ff-241">ObjectID</span></span> |<span data-ttu-id="019ff-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="019ff-242">String</span></span> |
| <span data-ttu-id="019ff-243">Ciąg</span><span class="sxs-lookup"><span data-stu-id="019ff-243">String</span></span> |<span data-ttu-id="019ff-244">Ciąg</span><span class="sxs-lookup"><span data-stu-id="019ff-244">String</span></span> |
| <span data-ttu-id="019ff-245">IDENTYFIKATOR UUID</span><span class="sxs-lookup"><span data-stu-id="019ff-245">UUID</span></span> |<span data-ttu-id="019ff-246">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="019ff-246">Guid</span></span> |
| <span data-ttu-id="019ff-247">Obiekt</span><span class="sxs-lookup"><span data-stu-id="019ff-247">Object</span></span> |<span data-ttu-id="019ff-248">Renormalized do spłaszczenia kolumn z "_" jako separatora zagnieżdżonych</span><span class="sxs-lookup"><span data-stu-id="019ff-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="019ff-249">toolearn o obsługę tablic za pomocą tabele wirtualne można znaleźć zbyt[obsługę złożonych typów przy użyciu tabele wirtualne](#support-for-complex-types-using-virtual-tables) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="019ff-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="019ff-250">Obecnie nie są obsługiwane następujące typy danych MongoDB hello: DBPointer, JavaScript, maksymalna liczba na minutę klucza, wyrażenie regularne, Symbol, Timestamp, niezdefiniowane</span><span class="sxs-lookup"><span data-stu-id="019ff-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="019ff-251">Obsługę złożonych typów przy użyciu tabele wirtualne</span><span class="sxs-lookup"><span data-stu-id="019ff-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="019ff-252">Fabryka danych Azure korzysta z wbudowanej ODBC sterownika tooconnect tooand kopiowania danych z bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="019ff-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="019ff-253">Typów złożonych takich jak macierze lub obiektów z różnymi typami wszystkich dokumentów hello sterownik hello ponownie normalizuje danych do odpowiednich tabel wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="019ff-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="019ff-254">W szczególności jeśli tabela zawiera takich kolumn, sterownik hello generuje hello następujące tabele wirtualne:</span><span class="sxs-lookup"><span data-stu-id="019ff-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="019ff-255">A **tabeli podstawowej**, który zawiera hello tych samych danych co hello rzeczywistych tabeli, z wyjątkiem hello kolumny typu złożonego.</span><span class="sxs-lookup"><span data-stu-id="019ff-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="019ff-256">tabeli podstawowej Hello używa hello takie same nazwy jako hello rzeczywistych tabeli, która reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="019ff-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="019ff-257">A **tabeli wirtualnej** dla każdej kolumny typu złożonego, która rozszerza hello zagnieżdżone dane.</span><span class="sxs-lookup"><span data-stu-id="019ff-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="019ff-258">tabele wirtualne Hello są nazywane przy użyciu hello Nazwa tabeli rzeczywistych hello, separator "_" i nazwą hello hello tablicy lub obiektu.</span><span class="sxs-lookup"><span data-stu-id="019ff-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="019ff-259">Tabele wirtualne odnoszą się toohello dane w tabeli rzeczywistych hello, włączanie tooaccess sterownika hello hello nieznormalizowany danych.</span><span class="sxs-lookup"><span data-stu-id="019ff-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="019ff-260">Zobacz przykład sekcję poniżej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="019ff-260">See Example section below details.</span></span> <span data-ttu-id="019ff-261">Dostęp z zawartości hello tablic bazy danych MongoDB, zapytań i przyłączanie tabel wirtualnego hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="019ff-262">Można użyć hello [kreatora kopiowania](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) widoku toointuitively hello listy tabel w bazie danych MongoDB, łącznie z tabelami wirtualnego hello i wyświetlić podgląd danych hello wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="019ff-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="019ff-263">Można również utworzyć zapytanie w hello kreatora kopiowania i sprawdź poprawność toosee hello wyniku.</span><span class="sxs-lookup"><span data-stu-id="019ff-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="019ff-264">Przykład</span><span class="sxs-lookup"><span data-stu-id="019ff-264">Example</span></span>
<span data-ttu-id="019ff-265">Na przykład "ExampleTable" poniżej znajduje się tabela bazy danych MongoDB o jedną kolumnę z tablicę obiektów w każdej komórce — faktury i jedną kolumnę z tablicą typów skalarnych — klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="019ff-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="019ff-266">_id</span><span class="sxs-lookup"><span data-stu-id="019ff-266">_id</span></span> | <span data-ttu-id="019ff-267">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="019ff-267">Customer Name</span></span> | <span data-ttu-id="019ff-268">Faktury</span><span class="sxs-lookup"><span data-stu-id="019ff-268">Invoices</span></span> | <span data-ttu-id="019ff-269">Poziom usług</span><span class="sxs-lookup"><span data-stu-id="019ff-269">Service Level</span></span> | <span data-ttu-id="019ff-270">Klasyfikacje</span><span class="sxs-lookup"><span data-stu-id="019ff-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="019ff-271">1111</span><span class="sxs-lookup"><span data-stu-id="019ff-271">1111</span></span> |<span data-ttu-id="019ff-272">ABC</span><span class="sxs-lookup"><span data-stu-id="019ff-272">ABC</span></span> |<span data-ttu-id="019ff-273">[{invoice_id: elementu "123",: "tostera", cena: Rabat "456",: "0,2"}, {invoice_id: "124", element: "piec", cena: Zniżka "1235": "0,2"}]</span><span class="sxs-lookup"><span data-stu-id="019ff-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="019ff-274">Srebrny</span><span class="sxs-lookup"><span data-stu-id="019ff-274">Silver</span></span> |<span data-ttu-id="019ff-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="019ff-275">[5,6]</span></span> |
| <span data-ttu-id="019ff-276">2222</span><span class="sxs-lookup"><span data-stu-id="019ff-276">2222</span></span> |<span data-ttu-id="019ff-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="019ff-277">XYZ</span></span> |<span data-ttu-id="019ff-278">[{invoice_id: element "135": "lodówko", cena: Rabat "12543": "0,0"}]</span><span class="sxs-lookup"><span data-stu-id="019ff-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="019ff-279">Gold</span><span class="sxs-lookup"><span data-stu-id="019ff-279">Gold</span></span> |<span data-ttu-id="019ff-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="019ff-280">[1,2]</span></span> |

<span data-ttu-id="019ff-281">Sterownik Hello powoduje wygenerowanie wielu toorepresent tabele wirtualne to pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="019ff-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="019ff-282">pierwszy tabeli wirtualnej Hello jest hello tabeli podstawowej o nazwie "ExampleTable", pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="019ff-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="019ff-283">Tabela podstawowa Hello zawiera wszystkie dane hello hello oryginalnej tabeli, ale hello danych z tablic hello została pominięta i jest rozwinięta w tabelach wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="019ff-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="019ff-284">_id</span><span class="sxs-lookup"><span data-stu-id="019ff-284">_id</span></span> | <span data-ttu-id="019ff-285">Nazwa klienta</span><span class="sxs-lookup"><span data-stu-id="019ff-285">Customer Name</span></span> | <span data-ttu-id="019ff-286">Poziom usług</span><span class="sxs-lookup"><span data-stu-id="019ff-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="019ff-287">1111</span><span class="sxs-lookup"><span data-stu-id="019ff-287">1111</span></span> |<span data-ttu-id="019ff-288">ABC</span><span class="sxs-lookup"><span data-stu-id="019ff-288">ABC</span></span> |<span data-ttu-id="019ff-289">Srebrny</span><span class="sxs-lookup"><span data-stu-id="019ff-289">Silver</span></span> |
| <span data-ttu-id="019ff-290">2222</span><span class="sxs-lookup"><span data-stu-id="019ff-290">2222</span></span> |<span data-ttu-id="019ff-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="019ff-291">XYZ</span></span> |<span data-ttu-id="019ff-292">Gold</span><span class="sxs-lookup"><span data-stu-id="019ff-292">Gold</span></span> |

<span data-ttu-id="019ff-293">Witaj w poniższych tabelach hello wirtualnego tabel, które reprezentują hello oryginalnego tablic, na przykład Witaj.</span><span class="sxs-lookup"><span data-stu-id="019ff-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="019ff-294">Te tabele zawierają hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="019ff-294">These tables contain hello following:</span></span>

* <span data-ttu-id="019ff-295">Odwołanie kopii toohello oryginalnego kolumna klucza podstawowego odpowiedni toohello wiersz tablicy oryginalnej hello (za pomocą kolumny _id hello)</span><span class="sxs-lookup"><span data-stu-id="019ff-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="019ff-296">Wskazanie pozycji hello danych hello w tablicy oryginalnej hello</span><span class="sxs-lookup"><span data-stu-id="019ff-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="019ff-297">dane dla każdego elementu w tablicy hello rozwinięty Hello</span><span class="sxs-lookup"><span data-stu-id="019ff-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="019ff-298">Tabela "ExampleTable_Invoices":</span><span class="sxs-lookup"><span data-stu-id="019ff-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="019ff-299">_id</span><span class="sxs-lookup"><span data-stu-id="019ff-299">_id</span></span> | <span data-ttu-id="019ff-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="019ff-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="019ff-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="019ff-301">invoice_id</span></span> | <span data-ttu-id="019ff-302">Element</span><span class="sxs-lookup"><span data-stu-id="019ff-302">item</span></span> | <span data-ttu-id="019ff-303">price</span><span class="sxs-lookup"><span data-stu-id="019ff-303">price</span></span> | <span data-ttu-id="019ff-304">Rabat</span><span class="sxs-lookup"><span data-stu-id="019ff-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="019ff-305">1111</span><span class="sxs-lookup"><span data-stu-id="019ff-305">1111</span></span> |<span data-ttu-id="019ff-306">0</span><span class="sxs-lookup"><span data-stu-id="019ff-306">0</span></span> |<span data-ttu-id="019ff-307">123</span><span class="sxs-lookup"><span data-stu-id="019ff-307">123</span></span> |<span data-ttu-id="019ff-308">tostera</span><span class="sxs-lookup"><span data-stu-id="019ff-308">toaster</span></span> |<span data-ttu-id="019ff-309">456</span><span class="sxs-lookup"><span data-stu-id="019ff-309">456</span></span> |<span data-ttu-id="019ff-310">0.2</span><span class="sxs-lookup"><span data-stu-id="019ff-310">0.2</span></span> |
| <span data-ttu-id="019ff-311">1111</span><span class="sxs-lookup"><span data-stu-id="019ff-311">1111</span></span> |<span data-ttu-id="019ff-312">1</span><span class="sxs-lookup"><span data-stu-id="019ff-312">1</span></span> |<span data-ttu-id="019ff-313">124</span><span class="sxs-lookup"><span data-stu-id="019ff-313">124</span></span> |<span data-ttu-id="019ff-314">Piec</span><span class="sxs-lookup"><span data-stu-id="019ff-314">oven</span></span> |<span data-ttu-id="019ff-315">1235</span><span class="sxs-lookup"><span data-stu-id="019ff-315">1235</span></span> |<span data-ttu-id="019ff-316">0.2</span><span class="sxs-lookup"><span data-stu-id="019ff-316">0.2</span></span> |
| <span data-ttu-id="019ff-317">2222</span><span class="sxs-lookup"><span data-stu-id="019ff-317">2222</span></span> |<span data-ttu-id="019ff-318">0</span><span class="sxs-lookup"><span data-stu-id="019ff-318">0</span></span> |<span data-ttu-id="019ff-319">135</span><span class="sxs-lookup"><span data-stu-id="019ff-319">135</span></span> |<span data-ttu-id="019ff-320">lodówko</span><span class="sxs-lookup"><span data-stu-id="019ff-320">fridge</span></span> |<span data-ttu-id="019ff-321">12543</span><span class="sxs-lookup"><span data-stu-id="019ff-321">12543</span></span> |<span data-ttu-id="019ff-322">0.0</span><span class="sxs-lookup"><span data-stu-id="019ff-322">0.0</span></span> |

<span data-ttu-id="019ff-323">Tabela "ExampleTable_Ratings":</span><span class="sxs-lookup"><span data-stu-id="019ff-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="019ff-324">_id</span><span class="sxs-lookup"><span data-stu-id="019ff-324">_id</span></span> | <span data-ttu-id="019ff-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="019ff-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="019ff-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="019ff-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="019ff-327">1111</span><span class="sxs-lookup"><span data-stu-id="019ff-327">1111</span></span> |<span data-ttu-id="019ff-328">0</span><span class="sxs-lookup"><span data-stu-id="019ff-328">0</span></span> |<span data-ttu-id="019ff-329">5</span><span class="sxs-lookup"><span data-stu-id="019ff-329">5</span></span> |
| <span data-ttu-id="019ff-330">1111</span><span class="sxs-lookup"><span data-stu-id="019ff-330">1111</span></span> |<span data-ttu-id="019ff-331">1</span><span class="sxs-lookup"><span data-stu-id="019ff-331">1</span></span> |<span data-ttu-id="019ff-332">6</span><span class="sxs-lookup"><span data-stu-id="019ff-332">6</span></span> |
| <span data-ttu-id="019ff-333">2222</span><span class="sxs-lookup"><span data-stu-id="019ff-333">2222</span></span> |<span data-ttu-id="019ff-334">0</span><span class="sxs-lookup"><span data-stu-id="019ff-334">0</span></span> |<span data-ttu-id="019ff-335">1</span><span class="sxs-lookup"><span data-stu-id="019ff-335">1</span></span> |
| <span data-ttu-id="019ff-336">2222</span><span class="sxs-lookup"><span data-stu-id="019ff-336">2222</span></span> |<span data-ttu-id="019ff-337">1</span><span class="sxs-lookup"><span data-stu-id="019ff-337">1</span></span> |<span data-ttu-id="019ff-338">2</span><span class="sxs-lookup"><span data-stu-id="019ff-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="019ff-339">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="019ff-339">Map source toosink columns</span></span>
<span data-ttu-id="019ff-340">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="019ff-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="019ff-341">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="019ff-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="019ff-342">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="019ff-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="019ff-343">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="019ff-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="019ff-344">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="019ff-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="019ff-345">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="019ff-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="019ff-346">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="019ff-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="019ff-347">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="019ff-347">Performance and Tuning</span></span>
<span data-ttu-id="019ff-348">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="019ff-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="019ff-349">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="019ff-349">Next Steps</span></span>
<span data-ttu-id="019ff-350">Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykuł instrukcje krok po kroku dla tworzenie potoku danych, które przenosi dane z lokalnymi danymi przechowywania tooan magazynu danych Azure.</span><span class="sxs-lookup"><span data-stu-id="019ff-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
