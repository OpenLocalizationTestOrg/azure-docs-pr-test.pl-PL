---
title: "dane aaaMove z Cassandra przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z Cassandra lokalnej bazy danych przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="50e08-103">Przenoszenia danych z Cassandra lokalną bazą danych przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="50e08-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="50e08-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="50e08-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="50e08-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="50e08-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="50e08-106">Można skopiować danych z lokalnego Cassandra magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="50e08-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="50e08-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="50e08-108">Fabryka danych aktualnie obsługuje tylko przeniesienie magazynu danych z danych Cassandra tooother magazyny danych, ale nie do przenoszenia danych z magazynu magazynów danych Cassandra tooa innych danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="50e08-109">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="50e08-109">Supported versions</span></span>
<span data-ttu-id="50e08-110">Łącznik Cassandra Hello obsługuje następujące wersje Cassandra hello: 2.X.</span><span class="sxs-lookup"><span data-stu-id="50e08-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50e08-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="50e08-111">Prerequisites</span></span>
<span data-ttu-id="50e08-112">Witaj fabryki danych Azure toobe stanie tooconnect tooyour lokalnymi Cassandra bazy danych usługi, należy zainstalować bramę zarządzania danymi na powitania sam komputera bazy danych hostów hello lub tooavoid osobnym komputerze fizycznym, konkurowanie o zasoby z hello Baza danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="50e08-113">Brama zarządzania danymi jest składnikiem, który łączy usługi toocloud źródeł danych lokalnych w sposób bezpieczny i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="50e08-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="50e08-114">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="50e08-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="50e08-115">Zobacz [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy hello toomove potoku danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="50e08-116">Należy użyć bazy danych hello bramy tooconnect tooa Cassandra, nawet jeśli hello baza danych znajduje się w chmurze hello, na przykład na maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="50e08-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="50e08-117">Y, do których masz hello bramy na hello tej bazy danych hello hostów w tej samej maszyny Wirtualnej lub na oddzielnym maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="50e08-118">Po zainstalowaniu bramy hello automatycznie instaluje bazę tooCassandra tooconnect sterownik ODBC Cassandra firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="50e08-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="50e08-119">W związku z tym nie ma potrzeby toomanually zainstalowania sterownika na komputerze bramy hello podczas kopiowania danych z bazy danych Cassandra hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="50e08-120">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="50e08-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="50e08-121">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="50e08-121">Getting started</span></span>
<span data-ttu-id="50e08-122">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="50e08-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="50e08-123">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="50e08-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="50e08-124">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="50e08-125">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="50e08-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="50e08-126">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="50e08-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="50e08-127">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="50e08-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="50e08-128">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="50e08-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="50e08-129">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="50e08-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="50e08-130">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="50e08-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="50e08-131">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="50e08-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="50e08-132">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="50e08-133">Przykładowy z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego magazynu danych Cassandra [przykład JSON: kopiowanie danych z tooAzure Cassandra obiektu Blob](#json-example-copy-data-from-cassandra-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="50e08-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="50e08-134">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych Cassandra tooa określonych jednostek fabryki danych używanych toodefine:</span><span class="sxs-lookup"><span data-stu-id="50e08-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="50e08-135">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="50e08-135">Linked service properties</span></span>
<span data-ttu-id="50e08-136">Hello w poniższej tabeli przedstawiono opis usługi określonego tooCassandra połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="50e08-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="50e08-137">Właściwość</span><span class="sxs-lookup"><span data-stu-id="50e08-137">Property</span></span> | <span data-ttu-id="50e08-138">Opis</span><span class="sxs-lookup"><span data-stu-id="50e08-138">Description</span></span> | <span data-ttu-id="50e08-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="50e08-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50e08-140">type</span><span class="sxs-lookup"><span data-stu-id="50e08-140">type</span></span> |<span data-ttu-id="50e08-141">musi mieć ustawioną właściwość type Hello: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="50e08-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="50e08-142">Tak</span><span class="sxs-lookup"><span data-stu-id="50e08-142">Yes</span></span> |
| <span data-ttu-id="50e08-143">Host</span><span class="sxs-lookup"><span data-stu-id="50e08-143">host</span></span> |<span data-ttu-id="50e08-144">Jeden lub więcej adresów IP lub nazw hostów serwerów Cassandra.</span><span class="sxs-lookup"><span data-stu-id="50e08-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="50e08-145">Określ rozdzielaną przecinkami listę adresów IP lub serwerów tooall tooconnect nazwy hosta jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="50e08-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="50e08-146">Tak</span><span class="sxs-lookup"><span data-stu-id="50e08-146">Yes</span></span> |
| <span data-ttu-id="50e08-147">port</span><span class="sxs-lookup"><span data-stu-id="50e08-147">port</span></span> |<span data-ttu-id="50e08-148">Hello port TCP, którego hello Cassandra serwer używa toolisten dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="50e08-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="50e08-149">Nie, wartość domyślna: 9042</span><span class="sxs-lookup"><span data-stu-id="50e08-149">No, default value: 9042</span></span> |
| <span data-ttu-id="50e08-150">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="50e08-150">authenticationType</span></span> |<span data-ttu-id="50e08-151">Podstawowa lub anonimowe</span><span class="sxs-lookup"><span data-stu-id="50e08-151">Basic, or Anonymous</span></span> |<span data-ttu-id="50e08-152">Tak</span><span class="sxs-lookup"><span data-stu-id="50e08-152">Yes</span></span> |
| <span data-ttu-id="50e08-153">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="50e08-153">username</span></span> |<span data-ttu-id="50e08-154">Określ nazwę użytkownika dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="50e08-155">Tak, jeśli authenticationType ustawiono tooBasic.</span><span class="sxs-lookup"><span data-stu-id="50e08-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="50e08-156">hasło</span><span class="sxs-lookup"><span data-stu-id="50e08-156">password</span></span> |<span data-ttu-id="50e08-157">Określ hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-157">Specify password for hello user account.</span></span> |<span data-ttu-id="50e08-158">Tak, jeśli authenticationType ustawiono tooBasic.</span><span class="sxs-lookup"><span data-stu-id="50e08-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="50e08-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="50e08-159">gatewayName</span></span> |<span data-ttu-id="50e08-160">Nazwa Hello hello bramy, która jest używana tooconnect toohello lokalnymi Cassandra w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="50e08-161">Tak</span><span class="sxs-lookup"><span data-stu-id="50e08-161">Yes</span></span> |
| <span data-ttu-id="50e08-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="50e08-162">encryptedCredential</span></span> |<span data-ttu-id="50e08-163">Poświadczenie szyfrowane przez bramę hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="50e08-164">Nie</span><span class="sxs-lookup"><span data-stu-id="50e08-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="50e08-165">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="50e08-165">Dataset properties</span></span>
<span data-ttu-id="50e08-166">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="50e08-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="50e08-167">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="50e08-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="50e08-168">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="50e08-169">Witaj typeProperties sekcja dla zestawu danych typu **CassandraTable** ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="50e08-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="50e08-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="50e08-170">Property</span></span> | <span data-ttu-id="50e08-171">Opis</span><span class="sxs-lookup"><span data-stu-id="50e08-171">Description</span></span> | <span data-ttu-id="50e08-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="50e08-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50e08-173">przestrzeni kluczy</span><span class="sxs-lookup"><span data-stu-id="50e08-173">keyspace</span></span> |<span data-ttu-id="50e08-174">Nazwa schematu bazy danych Cassandra lub hello przestrzeni kluczy.</span><span class="sxs-lookup"><span data-stu-id="50e08-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="50e08-175">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="50e08-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="50e08-176">tableName</span><span class="sxs-lookup"><span data-stu-id="50e08-176">tableName</span></span> |<span data-ttu-id="50e08-177">Nazwa tabeli hello Cassandra bazy danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="50e08-178">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="50e08-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="50e08-179">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="50e08-179">Copy activity properties</span></span>
<span data-ttu-id="50e08-180">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="50e08-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="50e08-181">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="50e08-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="50e08-182">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="50e08-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="50e08-183">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="50e08-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="50e08-184">Jeśli źródło jest typu **CassandraSource**, hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="50e08-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="50e08-185">Właściwość</span><span class="sxs-lookup"><span data-stu-id="50e08-185">Property</span></span> | <span data-ttu-id="50e08-186">Opis</span><span class="sxs-lookup"><span data-stu-id="50e08-186">Description</span></span> | <span data-ttu-id="50e08-187">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="50e08-187">Allowed values</span></span> | <span data-ttu-id="50e08-188">Wymagane</span><span class="sxs-lookup"><span data-stu-id="50e08-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50e08-189">query</span><span class="sxs-lookup"><span data-stu-id="50e08-189">query</span></span> |<span data-ttu-id="50e08-190">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="50e08-191">Zapytania SQL 92 lub CQL zapytania.</span><span class="sxs-lookup"><span data-stu-id="50e08-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="50e08-192">Zobacz [odwołania CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="50e08-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="50e08-193">Korzystając z zapytania SQL, określ **nazwa name.table przestrzeni kluczy** toorepresent hello tabelę, która ma tooquery.</span><span class="sxs-lookup"><span data-stu-id="50e08-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="50e08-194">Nie (jeśli są zdefiniowane tableName oraz przestrzeni kluczy w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="50e08-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="50e08-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="50e08-195">consistencyLevel</span></span> |<span data-ttu-id="50e08-196">poziomu spójności Hello Określa, ile replik musi odpowiadać żądanie odczytu tooa przed zwróceniem aplikacji klienckiej toohello danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="50e08-197">Sprawdzanie Cassandra hello określonej liczby replik dla żądania odczytu hello toosatisfy danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="50e08-198">JEDNĄ, DWIE, TRZY, KWORUM, WSZYSTKIE, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="50e08-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="50e08-199">Zobacz [Konfigurowanie spójność danych](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="50e08-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="50e08-200">Nie.</span><span class="sxs-lookup"><span data-stu-id="50e08-200">No.</span></span> <span data-ttu-id="50e08-201">Domyślna wartość to jeden.</span><span class="sxs-lookup"><span data-stu-id="50e08-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="50e08-202">Przykład JSON: kopiowanie danych z tooAzure Cassandra obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="50e08-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="50e08-203">W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="50e08-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="50e08-204">Pokazuje, jak dane toocopy z Cassandra lokalnej bazy danych tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="50e08-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="50e08-205">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="50e08-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50e08-206">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="50e08-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="50e08-207">Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="50e08-208">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="50e08-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="50e08-209">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="50e08-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="50e08-210">Połączonej usługi typu [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50e08-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="50e08-211">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="50e08-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="50e08-212">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50e08-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="50e08-213">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="50e08-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="50e08-214">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [CassandraSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="50e08-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="50e08-215">**Cassandra połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="50e08-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="50e08-216">W tym przykładzie użyto hello **Cassandra** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="50e08-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="50e08-217">Zobacz [Cassandra połączona usługa](#linked-service-properties) sekcji właściwości hello obsługiwane przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="50e08-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

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

<span data-ttu-id="50e08-218">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="50e08-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="50e08-219">**Zestaw danych wejściowych Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="50e08-219">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="50e08-220">Ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="50e08-221">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="50e08-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="50e08-222">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="50e08-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="50e08-223">**Aktywność kopiowania w potoku z Cassandra źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="50e08-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="50e08-224">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="50e08-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="50e08-225">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**CassandraSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="50e08-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="50e08-226">Zobacz [właściwości typu RelationalSource](#copy-activity-properties) hello listę obsługiwanych przez hello RelationalSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="50e08-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Cassandra tooan Azure blob",
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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="50e08-227">Mapowanie typu dla Cassandra</span><span class="sxs-lookup"><span data-stu-id="50e08-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="50e08-228">Typ Cassandra</span><span class="sxs-lookup"><span data-stu-id="50e08-228">Cassandra Type</span></span> | <span data-ttu-id="50e08-229">Typ na podstawie .net</span><span class="sxs-lookup"><span data-stu-id="50e08-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="50e08-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="50e08-230">ASCII</span></span> |<span data-ttu-id="50e08-231">Ciąg</span><span class="sxs-lookup"><span data-stu-id="50e08-231">String</span></span> |
| <span data-ttu-id="50e08-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="50e08-232">BIGINT</span></span> |<span data-ttu-id="50e08-233">Int64</span><span class="sxs-lookup"><span data-stu-id="50e08-233">Int64</span></span> |
| <span data-ttu-id="50e08-234">OBIEKT BLOB</span><span class="sxs-lookup"><span data-stu-id="50e08-234">BLOB</span></span> |<span data-ttu-id="50e08-235">Byte]</span><span class="sxs-lookup"><span data-stu-id="50e08-235">Byte[]</span></span> |
| <span data-ttu-id="50e08-236">WARTOŚĆ LOGICZNA</span><span class="sxs-lookup"><span data-stu-id="50e08-236">BOOLEAN</span></span> |<span data-ttu-id="50e08-237">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="50e08-237">Boolean</span></span> |
| <span data-ttu-id="50e08-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="50e08-238">DECIMAL</span></span> |<span data-ttu-id="50e08-239">Decimal</span><span class="sxs-lookup"><span data-stu-id="50e08-239">Decimal</span></span> |
| <span data-ttu-id="50e08-240">O PODWÓJNEJ PRECYZJI</span><span class="sxs-lookup"><span data-stu-id="50e08-240">DOUBLE</span></span> |<span data-ttu-id="50e08-241">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="50e08-241">Double</span></span> |
| <span data-ttu-id="50e08-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="50e08-242">FLOAT</span></span> |<span data-ttu-id="50e08-243">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="50e08-243">Single</span></span> |
| <span data-ttu-id="50e08-244">INET</span><span class="sxs-lookup"><span data-stu-id="50e08-244">INET</span></span> |<span data-ttu-id="50e08-245">Ciąg</span><span class="sxs-lookup"><span data-stu-id="50e08-245">String</span></span> |
| <span data-ttu-id="50e08-246">INT</span><span class="sxs-lookup"><span data-stu-id="50e08-246">INT</span></span> |<span data-ttu-id="50e08-247">Int32</span><span class="sxs-lookup"><span data-stu-id="50e08-247">Int32</span></span> |
| <span data-ttu-id="50e08-248">TEKST</span><span class="sxs-lookup"><span data-stu-id="50e08-248">TEXT</span></span> |<span data-ttu-id="50e08-249">Ciąg</span><span class="sxs-lookup"><span data-stu-id="50e08-249">String</span></span> |
| <span data-ttu-id="50e08-250">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="50e08-250">TIMESTAMP</span></span> |<span data-ttu-id="50e08-251">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="50e08-251">DateTime</span></span> |
| <span data-ttu-id="50e08-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="50e08-252">TIMEUUID</span></span> |<span data-ttu-id="50e08-253">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="50e08-253">Guid</span></span> |
| <span data-ttu-id="50e08-254">IDENTYFIKATOR UUID</span><span class="sxs-lookup"><span data-stu-id="50e08-254">UUID</span></span> |<span data-ttu-id="50e08-255">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="50e08-255">Guid</span></span> |
| <span data-ttu-id="50e08-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="50e08-256">VARCHAR</span></span> |<span data-ttu-id="50e08-257">Ciąg</span><span class="sxs-lookup"><span data-stu-id="50e08-257">String</span></span> |
| <span data-ttu-id="50e08-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="50e08-258">VARINT</span></span> |<span data-ttu-id="50e08-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="50e08-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="50e08-260">Kolekcja typów (mapy, zestaw, listy itp.), można znaleźć zbyt[współpracy z typami kolekcji Cassandra za pomocą tabeli wirtualnej](#work-with-collections-using-virtual-table) sekcji.</span><span class="sxs-lookup"><span data-stu-id="50e08-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="50e08-261">Typy definiowane przez użytkownika nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="50e08-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="50e08-262">Długość Hello długości kolumny typu Binary i kolumny typu String nie może być większa niż 4000.</span><span class="sxs-lookup"><span data-stu-id="50e08-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="50e08-263">Praca z kolekcji za pomocą tabeli wirtualnej</span><span class="sxs-lookup"><span data-stu-id="50e08-263">Work with collections using virtual table</span></span>
<span data-ttu-id="50e08-264">Fabryka danych Azure korzysta z wbudowanej ODBC sterownika tooconnect tooand kopiowania danych z bazy danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="50e08-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="50e08-265">Dla typów kolekcji, w tym mapy, zestaw i listy sterownik hello renormalizes hello danych do odpowiednich tabel wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="50e08-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="50e08-266">W szczególności jeśli tabela zawiera wszystkie kolumny w kolekcji, sterownik hello generuje hello następujące tabele wirtualne:</span><span class="sxs-lookup"><span data-stu-id="50e08-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="50e08-267">A **tabeli podstawowej**, który zawiera hello tych samych danych co hello rzeczywistych tabeli, z wyjątkiem hello kolekcji kolumn.</span><span class="sxs-lookup"><span data-stu-id="50e08-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="50e08-268">tabeli podstawowej Hello używa hello takie same nazwy jako hello rzeczywistych tabeli, która reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="50e08-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="50e08-269">A **tabeli wirtualnej** dla każdej kolekcji kolumny, która rozszerza hello zagnieżdżone dane.</span><span class="sxs-lookup"><span data-stu-id="50e08-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="50e08-270">tabele wirtualne Hello reprezentujących kolekcje są nazywane przy użyciu nazwy hello hello rzeczywistych tabeli separator "*vt*" i nazwę hello hello kolumny.</span><span class="sxs-lookup"><span data-stu-id="50e08-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="50e08-271">Tabele wirtualne odnoszą się toohello dane w tabeli rzeczywistych hello, włączanie tooaccess sterownika hello hello nieznormalizowany danych.</span><span class="sxs-lookup"><span data-stu-id="50e08-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="50e08-272">Zobacz sekcję przykład, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="50e08-272">See Example section for details.</span></span> <span data-ttu-id="50e08-273">Dostęp z zawartości hello Cassandra kolekcji, zapytań i przyłączanie tabel wirtualnego hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="50e08-274">Można użyć hello [kreatora kopiowania](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) widoku toointuitively hello listy tabel w bazie danych Cassandra tym tabele wirtualne hello i wyświetlić podgląd danych hello wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="50e08-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="50e08-275">Można również utworzyć zapytanie w hello kreatora kopiowania i sprawdź poprawność toosee hello wyniku.</span><span class="sxs-lookup"><span data-stu-id="50e08-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="50e08-276">Przykład</span><span class="sxs-lookup"><span data-stu-id="50e08-276">Example</span></span>
<span data-ttu-id="50e08-277">Na przykład hello następujące "ExampleTable" jest Cassandra tabeli bazy danych, która zawiera całkowitą kolumna klucza podstawowego o nazwie "pk_int", kolumna tekst o nazwie wartość kolumny listy, kolumny mapy i zestawu kolumn (o nazwie "StringSet").</span><span class="sxs-lookup"><span data-stu-id="50e08-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="50e08-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="50e08-278">pk_int</span></span> | <span data-ttu-id="50e08-279">Wartość</span><span class="sxs-lookup"><span data-stu-id="50e08-279">Value</span></span> | <span data-ttu-id="50e08-280">List</span><span class="sxs-lookup"><span data-stu-id="50e08-280">List</span></span> | <span data-ttu-id="50e08-281">mapy</span><span class="sxs-lookup"><span data-stu-id="50e08-281">Map</span></span> | <span data-ttu-id="50e08-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="50e08-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="50e08-283">1</span><span class="sxs-lookup"><span data-stu-id="50e08-283">1</span></span> |<span data-ttu-id="50e08-284">"Przykładowa wartość 1"</span><span class="sxs-lookup"><span data-stu-id="50e08-284">"sample value 1"</span></span> |<span data-ttu-id="50e08-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="50e08-285">["1", "2", "3"]</span></span> |<span data-ttu-id="50e08-286">{"S1": "", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="50e08-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="50e08-287">{"", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="50e08-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="50e08-288">3</span><span class="sxs-lookup"><span data-stu-id="50e08-288">3</span></span> |<span data-ttu-id="50e08-289">"przykład value 3"</span><span class="sxs-lookup"><span data-stu-id="50e08-289">"sample value 3"</span></span> |<span data-ttu-id="50e08-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="50e08-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="50e08-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="50e08-291">{"S1": "t"}</span></span> |<span data-ttu-id="50e08-292">{"", "E"}</span><span class="sxs-lookup"><span data-stu-id="50e08-292">{"A", "E"}</span></span> |

<span data-ttu-id="50e08-293">Sterownik Hello powoduje wygenerowanie wielu toorepresent tabele wirtualne to pojedynczej tabeli.</span><span class="sxs-lookup"><span data-stu-id="50e08-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="50e08-294">Witaj kolumny klucza obcego w tabelach wirtualnych hello odwoływania się do hello kolumn klucza podstawowego w tabeli rzeczywistych hello i wskazywać rzeczywistych, które odpowiada wiersza tabeli wirtualnej hello wiersza tabeli.</span><span class="sxs-lookup"><span data-stu-id="50e08-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="50e08-295">pierwszy tabeli wirtualnej Hello jest hello tabeli podstawowej o nazwie "ExampleTable" jest wyświetlany w obszarze hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="50e08-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="50e08-296">Tabela bazowa Hello zawiera hello tych samych danych co hello oryginalnej tabeli bazy danych, z wyjątkiem hello kolekcje, które są pominięte w tej tabeli i rozwinięty w innych tabelach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="50e08-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="50e08-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="50e08-297">pk_int</span></span> | <span data-ttu-id="50e08-298">Wartość</span><span class="sxs-lookup"><span data-stu-id="50e08-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="50e08-299">1</span><span class="sxs-lookup"><span data-stu-id="50e08-299">1</span></span> |<span data-ttu-id="50e08-300">"Przykładowa wartość 1"</span><span class="sxs-lookup"><span data-stu-id="50e08-300">"sample value 1"</span></span> |
| <span data-ttu-id="50e08-301">3</span><span class="sxs-lookup"><span data-stu-id="50e08-301">3</span></span> |<span data-ttu-id="50e08-302">"przykład value 3"</span><span class="sxs-lookup"><span data-stu-id="50e08-302">"sample value 3"</span></span> |

<span data-ttu-id="50e08-303">Witaj w poniższych tabelach hello tabel wirtualnych, które renormalize hello dane z kolumny listy, mapy i StringSet hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="50e08-304">Witaj kolumny o nazwach kończyć "_index" lub "_klucza" wskazać pozycję hello hello danych w oryginalnej listy hello lub mapy.</span><span class="sxs-lookup"><span data-stu-id="50e08-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="50e08-305">Witaj kolumny o nazwach kończących się znakiem "_value" zawierają dane hello rozwinięty z kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="50e08-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="50e08-306">Tabela "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="50e08-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="50e08-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="50e08-307">pk_int</span></span> | <span data-ttu-id="50e08-308">List_index</span><span class="sxs-lookup"><span data-stu-id="50e08-308">List_index</span></span> | <span data-ttu-id="50e08-309">List_value</span><span class="sxs-lookup"><span data-stu-id="50e08-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50e08-310">1</span><span class="sxs-lookup"><span data-stu-id="50e08-310">1</span></span> |<span data-ttu-id="50e08-311">0</span><span class="sxs-lookup"><span data-stu-id="50e08-311">0</span></span> |<span data-ttu-id="50e08-312">1</span><span class="sxs-lookup"><span data-stu-id="50e08-312">1</span></span> |
| <span data-ttu-id="50e08-313">1</span><span class="sxs-lookup"><span data-stu-id="50e08-313">1</span></span> |<span data-ttu-id="50e08-314">1</span><span class="sxs-lookup"><span data-stu-id="50e08-314">1</span></span> |<span data-ttu-id="50e08-315">2</span><span class="sxs-lookup"><span data-stu-id="50e08-315">2</span></span> |
| <span data-ttu-id="50e08-316">1</span><span class="sxs-lookup"><span data-stu-id="50e08-316">1</span></span> |<span data-ttu-id="50e08-317">2</span><span class="sxs-lookup"><span data-stu-id="50e08-317">2</span></span> |<span data-ttu-id="50e08-318">3</span><span class="sxs-lookup"><span data-stu-id="50e08-318">3</span></span> |
| <span data-ttu-id="50e08-319">3</span><span class="sxs-lookup"><span data-stu-id="50e08-319">3</span></span> |<span data-ttu-id="50e08-320">0</span><span class="sxs-lookup"><span data-stu-id="50e08-320">0</span></span> |<span data-ttu-id="50e08-321">100</span><span class="sxs-lookup"><span data-stu-id="50e08-321">100</span></span> |
| <span data-ttu-id="50e08-322">3</span><span class="sxs-lookup"><span data-stu-id="50e08-322">3</span></span> |<span data-ttu-id="50e08-323">1</span><span class="sxs-lookup"><span data-stu-id="50e08-323">1</span></span> |<span data-ttu-id="50e08-324">101</span><span class="sxs-lookup"><span data-stu-id="50e08-324">101</span></span> |
| <span data-ttu-id="50e08-325">3</span><span class="sxs-lookup"><span data-stu-id="50e08-325">3</span></span> |<span data-ttu-id="50e08-326">2</span><span class="sxs-lookup"><span data-stu-id="50e08-326">2</span></span> |<span data-ttu-id="50e08-327">102</span><span class="sxs-lookup"><span data-stu-id="50e08-327">102</span></span> |
| <span data-ttu-id="50e08-328">3</span><span class="sxs-lookup"><span data-stu-id="50e08-328">3</span></span> |<span data-ttu-id="50e08-329">3</span><span class="sxs-lookup"><span data-stu-id="50e08-329">3</span></span> |<span data-ttu-id="50e08-330">103</span><span class="sxs-lookup"><span data-stu-id="50e08-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="50e08-331">Tabela "ExampleTable_vt_Map":</span><span class="sxs-lookup"><span data-stu-id="50e08-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="50e08-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="50e08-332">pk_int</span></span> | <span data-ttu-id="50e08-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="50e08-333">Map_key</span></span> | <span data-ttu-id="50e08-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="50e08-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50e08-335">1</span><span class="sxs-lookup"><span data-stu-id="50e08-335">1</span></span> |<span data-ttu-id="50e08-336">S1</span><span class="sxs-lookup"><span data-stu-id="50e08-336">S1</span></span> |<span data-ttu-id="50e08-337">A</span><span class="sxs-lookup"><span data-stu-id="50e08-337">A</span></span> |
| <span data-ttu-id="50e08-338">1</span><span class="sxs-lookup"><span data-stu-id="50e08-338">1</span></span> |<span data-ttu-id="50e08-339">S2</span><span class="sxs-lookup"><span data-stu-id="50e08-339">S2</span></span> |<span data-ttu-id="50e08-340">B</span><span class="sxs-lookup"><span data-stu-id="50e08-340">b</span></span> |
| <span data-ttu-id="50e08-341">3</span><span class="sxs-lookup"><span data-stu-id="50e08-341">3</span></span> |<span data-ttu-id="50e08-342">S1</span><span class="sxs-lookup"><span data-stu-id="50e08-342">S1</span></span> |<span data-ttu-id="50e08-343">T</span><span class="sxs-lookup"><span data-stu-id="50e08-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="50e08-344">Tabela "ExampleTable_vt_StringSet":</span><span class="sxs-lookup"><span data-stu-id="50e08-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="50e08-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="50e08-345">pk_int</span></span> | <span data-ttu-id="50e08-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="50e08-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="50e08-347">1</span><span class="sxs-lookup"><span data-stu-id="50e08-347">1</span></span> |<span data-ttu-id="50e08-348">A</span><span class="sxs-lookup"><span data-stu-id="50e08-348">A</span></span> |
| <span data-ttu-id="50e08-349">1</span><span class="sxs-lookup"><span data-stu-id="50e08-349">1</span></span> |<span data-ttu-id="50e08-350">B</span><span class="sxs-lookup"><span data-stu-id="50e08-350">B</span></span> |
| <span data-ttu-id="50e08-351">1</span><span class="sxs-lookup"><span data-stu-id="50e08-351">1</span></span> |<span data-ttu-id="50e08-352">C</span><span class="sxs-lookup"><span data-stu-id="50e08-352">C</span></span> |
| <span data-ttu-id="50e08-353">3</span><span class="sxs-lookup"><span data-stu-id="50e08-353">3</span></span> |<span data-ttu-id="50e08-354">A</span><span class="sxs-lookup"><span data-stu-id="50e08-354">A</span></span> |
| <span data-ttu-id="50e08-355">3</span><span class="sxs-lookup"><span data-stu-id="50e08-355">3</span></span> |<span data-ttu-id="50e08-356">E</span><span class="sxs-lookup"><span data-stu-id="50e08-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="50e08-357">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="50e08-357">Map source toosink columns</span></span>
<span data-ttu-id="50e08-358">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="50e08-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="50e08-359">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="50e08-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="50e08-360">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="50e08-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="50e08-361">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="50e08-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="50e08-362">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="50e08-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="50e08-363">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="50e08-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="50e08-364">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="50e08-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="50e08-365">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="50e08-365">Performance and Tuning</span></span>
<span data-ttu-id="50e08-366">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="50e08-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
