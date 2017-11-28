---
title: "aaaMove danych z PostgreSQL przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych z bazy danych PostgreSQL przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="25f6d-103">Przenoszenia danych z PostgreSQL przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="25f6d-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="25f6d-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="25f6d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="25f6d-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="25f6d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="25f6d-106">Można skopiować danych z lokalnego PostgreSQL magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="25f6d-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania hello, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="25f6d-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="25f6d-108">Fabryki danych obecnie obsługuje przenoszenia danych z PostgreSQL bazy danych tooother magazyny danych, ale nie do przenoszenia danych z innych danych przechowuje tooan bazą danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="25f6d-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="25f6d-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="25f6d-109">prerequisites</span></span>

<span data-ttu-id="25f6d-110">Usługi fabryka danych obsługuje łączenia źródeł PostgreSQL tooon lokalnych przy użyciu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="25f6d-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="25f6d-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="25f6d-112">Wymagana jest brama, nawet wtedy, gdy baza danych PostgreSQL hello znajduje się w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="25f6d-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="25f6d-113">Możesz zainstalować bramę na powitania sam maszyn wirtualnych IaaS jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="25f6d-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="25f6d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="25f6d-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="25f6d-115">Supported versions and installation</span></span>
<span data-ttu-id="25f6d-116">Brama zarządzania danymi tooconnect toohello PostgreSQL bazy danych, można zainstalować w hello [Ngpsql dostawcy danych PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 lub powyżej na hello sam system jako hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="25f6d-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="25f6d-117">PostgreSQL wersji 7.4 i nowszej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="25f6d-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="25f6d-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="25f6d-118">Getting started</span></span>
<span data-ttu-id="25f6d-119">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych PostgreSQL lokalnymi przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="25f6d-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="25f6d-120">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="25f6d-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="25f6d-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="25f6d-122">Można także użyć hello następujące narzędzia toocreate potoku:</span><span class="sxs-lookup"><span data-stu-id="25f6d-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="25f6d-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="25f6d-123">Azure portal</span></span>
    - <span data-ttu-id="25f6d-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="25f6d-124">Visual Studio</span></span>
    - <span data-ttu-id="25f6d-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="25f6d-125">Azure PowerShell</span></span>
    - <span data-ttu-id="25f6d-126">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25f6d-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="25f6d-127">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="25f6d-127">.NET API</span></span>
    - <span data-ttu-id="25f6d-128">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="25f6d-128">REST API</span></span>

     <span data-ttu-id="25f6d-129">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="25f6d-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="25f6d-130">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="25f6d-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="25f6d-131">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="25f6d-132">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="25f6d-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="25f6d-133">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="25f6d-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="25f6d-134">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="25f6d-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="25f6d-135">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="25f6d-136">Przykładowy z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego magazynu danych PostgreSQL [przykład JSON: kopiowanie danych z tooAzure PostgreSQL obiektu Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="25f6d-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="25f6d-137">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych PostgreSQL tooa określonych jednostek fabryki danych używanych toodefine:</span><span class="sxs-lookup"><span data-stu-id="25f6d-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="25f6d-138">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="25f6d-138">Linked service properties</span></span>
<span data-ttu-id="25f6d-139">Hello w poniższej tabeli przedstawiono opis usługi określonego tooPostgreSQL połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="25f6d-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="25f6d-140">Właściwość</span><span class="sxs-lookup"><span data-stu-id="25f6d-140">Property</span></span> | <span data-ttu-id="25f6d-141">Opis</span><span class="sxs-lookup"><span data-stu-id="25f6d-141">Description</span></span> | <span data-ttu-id="25f6d-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="25f6d-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25f6d-143">type</span><span class="sxs-lookup"><span data-stu-id="25f6d-143">type</span></span> |<span data-ttu-id="25f6d-144">musi mieć ustawioną właściwość type Hello: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="25f6d-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="25f6d-145">Tak</span><span class="sxs-lookup"><span data-stu-id="25f6d-145">Yes</span></span> |
| <span data-ttu-id="25f6d-146">serwer</span><span class="sxs-lookup"><span data-stu-id="25f6d-146">server</span></span> |<span data-ttu-id="25f6d-147">Nazwa serwera PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="25f6d-148">Tak</span><span class="sxs-lookup"><span data-stu-id="25f6d-148">Yes</span></span> |
| <span data-ttu-id="25f6d-149">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="25f6d-149">database</span></span> |<span data-ttu-id="25f6d-150">Nazwa bazy danych PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="25f6d-151">Tak</span><span class="sxs-lookup"><span data-stu-id="25f6d-151">Yes</span></span> |
| <span data-ttu-id="25f6d-152">Schemat</span><span class="sxs-lookup"><span data-stu-id="25f6d-152">schema</span></span> |<span data-ttu-id="25f6d-153">Nazwa schematu hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="25f6d-154">Nazwa schematu Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="25f6d-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="25f6d-155">Nie</span><span class="sxs-lookup"><span data-stu-id="25f6d-155">No</span></span> |
| <span data-ttu-id="25f6d-156">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="25f6d-156">authenticationType</span></span> |<span data-ttu-id="25f6d-157">Typ uwierzytelniania używany tooconnect toohello PostgreSQL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="25f6d-158">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="25f6d-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="25f6d-159">Tak</span><span class="sxs-lookup"><span data-stu-id="25f6d-159">Yes</span></span> |
| <span data-ttu-id="25f6d-160">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="25f6d-160">username</span></span> |<span data-ttu-id="25f6d-161">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="25f6d-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="25f6d-162">Nie</span><span class="sxs-lookup"><span data-stu-id="25f6d-162">No</span></span> |
| <span data-ttu-id="25f6d-163">hasło</span><span class="sxs-lookup"><span data-stu-id="25f6d-163">password</span></span> |<span data-ttu-id="25f6d-164">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25f6d-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="25f6d-165">Nie</span><span class="sxs-lookup"><span data-stu-id="25f6d-165">No</span></span> |
| <span data-ttu-id="25f6d-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="25f6d-166">gatewayName</span></span> |<span data-ttu-id="25f6d-167">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="25f6d-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="25f6d-168">Tak</span><span class="sxs-lookup"><span data-stu-id="25f6d-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="25f6d-169">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="25f6d-169">Dataset properties</span></span>
<span data-ttu-id="25f6d-170">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="25f6d-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="25f6d-171">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="25f6d-172">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="25f6d-173">Witaj typeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych PostgreSQL) ma następujące właściwości hello:</span><span class="sxs-lookup"><span data-stu-id="25f6d-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="25f6d-174">Właściwość</span><span class="sxs-lookup"><span data-stu-id="25f6d-174">Property</span></span> | <span data-ttu-id="25f6d-175">Opis</span><span class="sxs-lookup"><span data-stu-id="25f6d-175">Description</span></span> | <span data-ttu-id="25f6d-176">Wymagane</span><span class="sxs-lookup"><span data-stu-id="25f6d-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25f6d-177">tableName</span><span class="sxs-lookup"><span data-stu-id="25f6d-177">tableName</span></span> |<span data-ttu-id="25f6d-178">Nazwa tabeli hello w hello wystąpienie bazy danych PostgreSQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="25f6d-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="25f6d-179">Witaj tableName jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="25f6d-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="25f6d-180">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="25f6d-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="25f6d-181">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="25f6d-181">Copy activity properties</span></span>
<span data-ttu-id="25f6d-182">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="25f6d-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="25f6d-183">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="25f6d-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="25f6d-184">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="25f6d-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="25f6d-185">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="25f6d-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="25f6d-186">Jeśli źródło jest typu **RelationalSource** (która obejmuje PostgreSQL), hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="25f6d-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="25f6d-187">Właściwość</span><span class="sxs-lookup"><span data-stu-id="25f6d-187">Property</span></span> | <span data-ttu-id="25f6d-188">Opis</span><span class="sxs-lookup"><span data-stu-id="25f6d-188">Description</span></span> | <span data-ttu-id="25f6d-189">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="25f6d-189">Allowed values</span></span> | <span data-ttu-id="25f6d-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="25f6d-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="25f6d-191">query</span><span class="sxs-lookup"><span data-stu-id="25f6d-191">query</span></span> |<span data-ttu-id="25f6d-192">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="25f6d-193">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="25f6d-193">SQL query string.</span></span> <span data-ttu-id="25f6d-194">Na przykład: "zapytania": "Wybierz * z \"MySchema\".\" MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="25f6d-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="25f6d-195">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="25f6d-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="25f6d-196">Nazwy schematu i tabeli jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="25f6d-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="25f6d-197">Umieść je w `""` (podwójne cudzysłowy) w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="25f6d-198">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="25f6d-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="25f6d-199">Przykład JSON: kopiowanie danych z tooAzure PostgreSQL obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="25f6d-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="25f6d-200">W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="25f6d-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="25f6d-201">Przedstawiają sposób toocopy danych PostgreSQL bazy danych tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="25f6d-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="25f6d-202">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="25f6d-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="25f6d-203">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="25f6d-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="25f6d-204">Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="25f6d-205">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="25f6d-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="25f6d-206">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="25f6d-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="25f6d-207">Połączonej usługi typu [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="25f6d-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="25f6d-208">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="25f6d-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="25f6d-209">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="25f6d-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="25f6d-210">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="25f6d-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="25f6d-211">Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="25f6d-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="25f6d-212">przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa bazy danych PostgreSQL co godzinę.</span><span class="sxs-lookup"><span data-stu-id="25f6d-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="25f6d-213">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="25f6d-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="25f6d-214">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="25f6d-215">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="25f6d-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="25f6d-216">**PostgreSQL połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="25f6d-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
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
<span data-ttu-id="25f6d-217">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="25f6d-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="25f6d-218">**Wejściowy zestaw danych PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="25f6d-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="25f6d-219">przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" PostgreSQL i zawiera kolumnę o nazwie "timestamp" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="25f6d-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="25f6d-220">Ustawienie `"external": true` informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

<span data-ttu-id="25f6d-221">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="25f6d-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="25f6d-222">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="25f6d-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="25f6d-223">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="25f6d-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="25f6d-224">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="25f6d-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="25f6d-225">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="25f6d-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="25f6d-226">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="25f6d-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="25f6d-227">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="25f6d-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="25f6d-228">Zapytanie SQL Hello określone dla hello **zapytania** właściwości wybiera hello danych z tabeli public.usstates hello w bazie danych PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="25f6d-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="25f6d-229">Mapowanie typu dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="25f6d-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="25f6d-230">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="25f6d-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="25f6d-231">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="25f6d-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="25f6d-232">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="25f6d-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="25f6d-233">Podczas przenoszenia danych tooPostgreSQL, hello następujące mapowania są używane z PostgreSQL too.NET typu.</span><span class="sxs-lookup"><span data-stu-id="25f6d-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="25f6d-234">Typ bazy danych PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="25f6d-234">PostgreSQL Database type</span></span> | <span data-ttu-id="25f6d-235">Aliasy PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="25f6d-235">PostgresSQL aliases</span></span> | <span data-ttu-id="25f6d-236">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="25f6d-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25f6d-237">abstime</span><span class="sxs-lookup"><span data-stu-id="25f6d-237">abstime</span></span> | |<span data-ttu-id="25f6d-238">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="25f6d-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="25f6d-239">bigint</span><span class="sxs-lookup"><span data-stu-id="25f6d-239">bigint</span></span> |<span data-ttu-id="25f6d-240">int8</span><span class="sxs-lookup"><span data-stu-id="25f6d-240">int8</span></span> |<span data-ttu-id="25f6d-241">Int64</span><span class="sxs-lookup"><span data-stu-id="25f6d-241">Int64</span></span> |
| <span data-ttu-id="25f6d-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="25f6d-242">bigserial</span></span> |<span data-ttu-id="25f6d-243">serial8</span><span class="sxs-lookup"><span data-stu-id="25f6d-243">serial8</span></span> |<span data-ttu-id="25f6d-244">Int64</span><span class="sxs-lookup"><span data-stu-id="25f6d-244">Int64</span></span> |
| <span data-ttu-id="25f6d-245">bitowe [(n)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-245">bit [ (n) ]</span></span> | |<span data-ttu-id="25f6d-246">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="25f6d-247">bit zróżnicowanie [(n)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="25f6d-248">varbit</span><span class="sxs-lookup"><span data-stu-id="25f6d-248">varbit</span></span> |<span data-ttu-id="25f6d-249">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-249">Byte[], String</span></span> |
| <span data-ttu-id="25f6d-250">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="25f6d-250">boolean</span></span> |<span data-ttu-id="25f6d-251">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="25f6d-251">bool</span></span> |<span data-ttu-id="25f6d-252">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="25f6d-252">Boolean</span></span> |
| <span data-ttu-id="25f6d-253">Pole</span><span class="sxs-lookup"><span data-stu-id="25f6d-253">box</span></span> | |<span data-ttu-id="25f6d-254">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-255">bytea</span><span class="sxs-lookup"><span data-stu-id="25f6d-255">bytea</span></span> | |<span data-ttu-id="25f6d-256">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-257">znak [(n)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-257">character [ (n) ]</span></span> |<span data-ttu-id="25f6d-258">char [(n)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-258">char [ (n) ]</span></span> |<span data-ttu-id="25f6d-259">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-259">String</span></span> |
| <span data-ttu-id="25f6d-260">znak zróżnicowanie [(n)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-260">character varying [ (n) ]</span></span> |<span data-ttu-id="25f6d-261">varchar [(n)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-261">varchar [ (n) ]</span></span> |<span data-ttu-id="25f6d-262">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-262">String</span></span> |
| <span data-ttu-id="25f6d-263">CID</span><span class="sxs-lookup"><span data-stu-id="25f6d-263">cid</span></span> | |<span data-ttu-id="25f6d-264">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-264">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-265">CIDR</span><span class="sxs-lookup"><span data-stu-id="25f6d-265">cidr</span></span> | |<span data-ttu-id="25f6d-266">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-266">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-267">koło</span><span class="sxs-lookup"><span data-stu-id="25f6d-267">circle</span></span> | |<span data-ttu-id="25f6d-268">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-269">Data</span><span class="sxs-lookup"><span data-stu-id="25f6d-269">date</span></span> | |<span data-ttu-id="25f6d-270">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="25f6d-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="25f6d-271">DateRange</span><span class="sxs-lookup"><span data-stu-id="25f6d-271">daterange</span></span> | |<span data-ttu-id="25f6d-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-272">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-273">podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="25f6d-273">double precision</span></span> |<span data-ttu-id="25f6d-274">FLOAT8</span><span class="sxs-lookup"><span data-stu-id="25f6d-274">float8</span></span> |<span data-ttu-id="25f6d-275">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="25f6d-275">Double</span></span> |
| <span data-ttu-id="25f6d-276">inet</span><span class="sxs-lookup"><span data-stu-id="25f6d-276">inet</span></span> | |<span data-ttu-id="25f6d-277">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-278">intarry</span><span class="sxs-lookup"><span data-stu-id="25f6d-278">intarry</span></span> | |<span data-ttu-id="25f6d-279">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-279">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-280">int4range</span><span class="sxs-lookup"><span data-stu-id="25f6d-280">int4range</span></span> | |<span data-ttu-id="25f6d-281">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-281">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-282">int8range</span><span class="sxs-lookup"><span data-stu-id="25f6d-282">int8range</span></span> | |<span data-ttu-id="25f6d-283">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-283">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-284">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="25f6d-284">integer</span></span> |<span data-ttu-id="25f6d-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="25f6d-285">int, int4</span></span> |<span data-ttu-id="25f6d-286">Int32</span><span class="sxs-lookup"><span data-stu-id="25f6d-286">Int32</span></span> |
| <span data-ttu-id="25f6d-287">Interwał [pola] [(p)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="25f6d-288">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="25f6d-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="25f6d-289">JSON</span><span class="sxs-lookup"><span data-stu-id="25f6d-289">json</span></span> | |<span data-ttu-id="25f6d-290">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-290">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="25f6d-291">jsonb</span></span> | |<span data-ttu-id="25f6d-292">Byte]</span><span class="sxs-lookup"><span data-stu-id="25f6d-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="25f6d-293">wiersz</span><span class="sxs-lookup"><span data-stu-id="25f6d-293">line</span></span> | |<span data-ttu-id="25f6d-294">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-295">lseg</span><span class="sxs-lookup"><span data-stu-id="25f6d-295">lseg</span></span> | |<span data-ttu-id="25f6d-296">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="25f6d-297">macaddr</span></span> | |<span data-ttu-id="25f6d-298">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-299">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="25f6d-299">money</span></span> | |<span data-ttu-id="25f6d-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="25f6d-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="25f6d-301">numeryczne [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="25f6d-302">decimal [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="25f6d-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="25f6d-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="25f6d-303">Decimal</span></span> |
| <span data-ttu-id="25f6d-304">numrange</span><span class="sxs-lookup"><span data-stu-id="25f6d-304">numrange</span></span> | |<span data-ttu-id="25f6d-305">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-305">String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-306">Identyfikator OID</span><span class="sxs-lookup"><span data-stu-id="25f6d-306">oid</span></span> | |<span data-ttu-id="25f6d-307">Int32</span><span class="sxs-lookup"><span data-stu-id="25f6d-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="25f6d-308">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="25f6d-308">path</span></span> | |<span data-ttu-id="25f6d-309">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="25f6d-310">pg_lsn</span></span> | |<span data-ttu-id="25f6d-311">Int64</span><span class="sxs-lookup"><span data-stu-id="25f6d-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="25f6d-312">punkt</span><span class="sxs-lookup"><span data-stu-id="25f6d-312">point</span></span> | |<span data-ttu-id="25f6d-313">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-314">wielokąta</span><span class="sxs-lookup"><span data-stu-id="25f6d-314">polygon</span></span> | |<span data-ttu-id="25f6d-315">Byte [], ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="25f6d-316">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="25f6d-316">real</span></span> |<span data-ttu-id="25f6d-317">FLOAT4</span><span class="sxs-lookup"><span data-stu-id="25f6d-317">float4</span></span> |<span data-ttu-id="25f6d-318">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="25f6d-318">Single</span></span> |
| <span data-ttu-id="25f6d-319">smallint</span><span class="sxs-lookup"><span data-stu-id="25f6d-319">smallint</span></span> |<span data-ttu-id="25f6d-320">int2</span><span class="sxs-lookup"><span data-stu-id="25f6d-320">int2</span></span> |<span data-ttu-id="25f6d-321">Int16</span><span class="sxs-lookup"><span data-stu-id="25f6d-321">Int16</span></span> |
| <span data-ttu-id="25f6d-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="25f6d-322">smallserial</span></span> |<span data-ttu-id="25f6d-323">serial2</span><span class="sxs-lookup"><span data-stu-id="25f6d-323">serial2</span></span> |<span data-ttu-id="25f6d-324">Int16</span><span class="sxs-lookup"><span data-stu-id="25f6d-324">Int16</span></span> |
| <span data-ttu-id="25f6d-325">Szeregowe</span><span class="sxs-lookup"><span data-stu-id="25f6d-325">serial</span></span> |<span data-ttu-id="25f6d-326">serial4</span><span class="sxs-lookup"><span data-stu-id="25f6d-326">serial4</span></span> |<span data-ttu-id="25f6d-327">Int32</span><span class="sxs-lookup"><span data-stu-id="25f6d-327">Int32</span></span> |
| <span data-ttu-id="25f6d-328">Tekst</span><span class="sxs-lookup"><span data-stu-id="25f6d-328">text</span></span> | |<span data-ttu-id="25f6d-329">Ciąg</span><span class="sxs-lookup"><span data-stu-id="25f6d-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="25f6d-330">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="25f6d-330">Map source toosink columns</span></span>
<span data-ttu-id="25f6d-331">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="25f6d-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="25f6d-332">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="25f6d-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="25f6d-333">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="25f6d-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="25f6d-334">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="25f6d-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="25f6d-335">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="25f6d-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="25f6d-336">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="25f6d-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="25f6d-337">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="25f6d-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="25f6d-338">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="25f6d-338">Performance and Tuning</span></span>
<span data-ttu-id="25f6d-339">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="25f6d-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
