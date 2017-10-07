---
title: "aaaMove danych z programu Sybase przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych z bazy danych programu Sybase przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="71f4a-103">Przenoszenia danych z programu Sybase przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="71f4a-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="71f4a-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="71f4a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="71f4a-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="71f4a-106">Można skopiować danych z lokalnego programu Sybase magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="71f4a-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="71f4a-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="71f4a-108">Fabryka danych aktualnie obsługuje tylko przeniesienie tooother magazyny danych magazynu danych ze źródła danych programu Sybase, ale nie do przenoszenia danych z innym magazynie danych programu Sybase tooa danych magazynów.</span><span class="sxs-lookup"><span data-stu-id="71f4a-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="71f4a-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="71f4a-109">Prerequisites</span></span>
<span data-ttu-id="71f4a-110">Usługi fabryka danych obsługuje łączącego źródeł Sybase tooon lokalnych przy użyciu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="71f4a-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="71f4a-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="71f4a-112">Wymagana jest brama, nawet wtedy, gdy baza danych programu Sybase hello znajduje się w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="71f4a-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="71f4a-113">Możesz zainstalować bramę hello na powitania sam maszyn wirtualnych IaaS jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="71f4a-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="71f4a-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="71f4a-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="71f4a-115">Supported versions and installation</span></span>
<span data-ttu-id="71f4a-116">Dla bramy zarządzania danymi tooconnect toohello bazy danych programu Sybase, potrzebujesz tooinstall hello [dostawcy danych programu Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 lub powyżej na hello sam system jako hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="71f4a-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="71f4a-117">Sybase wersji 16 i nowszej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="71f4a-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="71f4a-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="71f4a-118">Getting started</span></span>
<span data-ttu-id="71f4a-119">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="71f4a-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="71f4a-120">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="71f4a-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="71f4a-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="71f4a-122">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="71f4a-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="71f4a-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="71f4a-124">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="71f4a-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="71f4a-125">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="71f4a-126">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="71f4a-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="71f4a-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="71f4a-128">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="71f4a-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="71f4a-129">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="71f4a-130">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych programu Sybase lokalnych, zobacz [przykład JSON: kopiowanie danych z programu Sybase tooAzure obiektu Blob](#json-example-copy-data-from-sybase-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="71f4a-131">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych programu Sybase tooa określonych jednostek używanych toodefine fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="71f4a-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="71f4a-132">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="71f4a-132">Linked service properties</span></span>
<span data-ttu-id="71f4a-133">Hello w poniższej tabeli przedstawiono opis usługi określonego tooSybase połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="71f4a-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="71f4a-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="71f4a-134">Property</span></span> | <span data-ttu-id="71f4a-135">Opis</span><span class="sxs-lookup"><span data-stu-id="71f4a-135">Description</span></span> | <span data-ttu-id="71f4a-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="71f4a-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71f4a-137">type</span><span class="sxs-lookup"><span data-stu-id="71f4a-137">type</span></span> |<span data-ttu-id="71f4a-138">musi mieć ustawioną właściwość type Hello: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="71f4a-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="71f4a-139">Tak</span><span class="sxs-lookup"><span data-stu-id="71f4a-139">Yes</span></span> |
| <span data-ttu-id="71f4a-140">serwer</span><span class="sxs-lookup"><span data-stu-id="71f4a-140">server</span></span> |<span data-ttu-id="71f4a-141">Nazwa serwera programu Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="71f4a-142">Tak</span><span class="sxs-lookup"><span data-stu-id="71f4a-142">Yes</span></span> |
| <span data-ttu-id="71f4a-143">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="71f4a-143">database</span></span> |<span data-ttu-id="71f4a-144">Nazwa bazy danych programu Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="71f4a-145">Tak</span><span class="sxs-lookup"><span data-stu-id="71f4a-145">Yes</span></span> |
| <span data-ttu-id="71f4a-146">Schemat</span><span class="sxs-lookup"><span data-stu-id="71f4a-146">schema</span></span> |<span data-ttu-id="71f4a-147">Nazwa schematu hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="71f4a-148">Nie</span><span class="sxs-lookup"><span data-stu-id="71f4a-148">No</span></span> |
| <span data-ttu-id="71f4a-149">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="71f4a-149">authenticationType</span></span> |<span data-ttu-id="71f4a-150">Typ uwierzytelniania używany toohello tooconnect baz danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="71f4a-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="71f4a-151">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="71f4a-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="71f4a-152">Tak</span><span class="sxs-lookup"><span data-stu-id="71f4a-152">Yes</span></span> |
| <span data-ttu-id="71f4a-153">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="71f4a-153">username</span></span> |<span data-ttu-id="71f4a-154">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="71f4a-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="71f4a-155">Nie</span><span class="sxs-lookup"><span data-stu-id="71f4a-155">No</span></span> |
| <span data-ttu-id="71f4a-156">hasło</span><span class="sxs-lookup"><span data-stu-id="71f4a-156">password</span></span> |<span data-ttu-id="71f4a-157">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="71f4a-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="71f4a-158">Nie</span><span class="sxs-lookup"><span data-stu-id="71f4a-158">No</span></span> |
| <span data-ttu-id="71f4a-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="71f4a-159">gatewayName</span></span> |<span data-ttu-id="71f4a-160">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="71f4a-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="71f4a-161">Tak</span><span class="sxs-lookup"><span data-stu-id="71f4a-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="71f4a-162">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="71f4a-162">Dataset properties</span></span>
<span data-ttu-id="71f4a-163">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="71f4a-164">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="71f4a-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="71f4a-165">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="71f4a-166">Witaj **typeProperties** sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych programu Sybase) ma następujące właściwości hello:</span><span class="sxs-lookup"><span data-stu-id="71f4a-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="71f4a-167">Właściwość</span><span class="sxs-lookup"><span data-stu-id="71f4a-167">Property</span></span> | <span data-ttu-id="71f4a-168">Opis</span><span class="sxs-lookup"><span data-stu-id="71f4a-168">Description</span></span> | <span data-ttu-id="71f4a-169">Wymagane</span><span class="sxs-lookup"><span data-stu-id="71f4a-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71f4a-170">tableName</span><span class="sxs-lookup"><span data-stu-id="71f4a-170">tableName</span></span> |<span data-ttu-id="71f4a-171">Nazwa tabeli hello w hello wystąpienie bazy danych programu Sybase, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="71f4a-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="71f4a-172">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="71f4a-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="71f4a-173">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="71f4a-173">Copy activity properties</span></span>
<span data-ttu-id="71f4a-174">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="71f4a-175">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="71f4a-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="71f4a-176">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="71f4a-177">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="71f4a-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="71f4a-178">Gdy źródło hello jest typu **RelationalSource** (która obejmuje Sybase), dostępne są następujące właściwości hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="71f4a-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="71f4a-179">Właściwość</span><span class="sxs-lookup"><span data-stu-id="71f4a-179">Property</span></span> | <span data-ttu-id="71f4a-180">Opis</span><span class="sxs-lookup"><span data-stu-id="71f4a-180">Description</span></span> | <span data-ttu-id="71f4a-181">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="71f4a-181">Allowed values</span></span> | <span data-ttu-id="71f4a-182">Wymagane</span><span class="sxs-lookup"><span data-stu-id="71f4a-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71f4a-183">query</span><span class="sxs-lookup"><span data-stu-id="71f4a-183">query</span></span> |<span data-ttu-id="71f4a-184">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="71f4a-185">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="71f4a-185">SQL query string.</span></span> <span data-ttu-id="71f4a-186">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="71f4a-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="71f4a-187">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="71f4a-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="71f4a-188">Przykład JSON: kopiowanie danych z programu Sybase tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="71f4a-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="71f4a-189">Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="71f4a-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="71f4a-190">Przedstawiają sposób toocopy danych z programu Sybase bazie danych tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="71f4a-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="71f4a-191">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="71f4a-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="71f4a-192">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="71f4a-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="71f4a-193">Połączonej usługi typu [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="71f4a-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="71f4a-194">Liked usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="71f4a-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="71f4a-195">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="71f4a-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="71f4a-196">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="71f4a-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="71f4a-197">Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="71f4a-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="71f4a-198">przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa bazy danych programu Sybase, co godzinę.</span><span class="sxs-lookup"><span data-stu-id="71f4a-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="71f4a-199">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="71f4a-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="71f4a-200">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="71f4a-201">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="71f4a-202">**Sybase połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="71f4a-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="71f4a-203">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="71f4a-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="71f4a-204">**Wejściowy zestaw danych programu Sybase:**</span><span class="sxs-lookup"><span data-stu-id="71f4a-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="71f4a-205">przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" Sybase i zawiera kolumnę o nazwie "timestamp" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="71f4a-206">Ustawienie "external": true usługi fabryka danych hello informuje, że ten zestaw danych jest zewnętrzne toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="71f4a-207">Zwróć uwagę, że hello **typu** hello połączonej usługi jest ustawiony na wartość: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="71f4a-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="71f4a-208">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="71f4a-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="71f4a-209">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="71f4a-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="71f4a-210">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="71f4a-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="71f4a-211">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="71f4a-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="71f4a-212">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="71f4a-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="71f4a-213">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="71f4a-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="71f4a-214">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="71f4a-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="71f4a-215">Zapytanie SQL Hello określone dla hello **zapytania** właściwości wybiera hello danych z hello Zarejestrowana. Tabela zamówień hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="71f4a-216">Mapowanie typu dla programu Sybase</span><span class="sxs-lookup"><span data-stu-id="71f4a-216">Type mapping for Sybase</span></span>
<span data-ttu-id="71f4a-217">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, hello działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="71f4a-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="71f4a-218">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="71f4a-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="71f4a-219">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="71f4a-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="71f4a-220">Sybase obsługuje T-SQL i typy T-SQL.</span><span class="sxs-lookup"><span data-stu-id="71f4a-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="71f4a-221">Dla tabeli mapowania z typu too.NET typy sql, zobacz [Łącznik usług SQL Azure](data-factory-azure-sql-connector.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="71f4a-222">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="71f4a-222">Map source toosink columns</span></span>
<span data-ttu-id="71f4a-223">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="71f4a-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="71f4a-224">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="71f4a-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="71f4a-225">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="71f4a-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="71f4a-226">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="71f4a-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="71f4a-227">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="71f4a-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="71f4a-228">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="71f4a-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="71f4a-229">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="71f4a-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="71f4a-230">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="71f4a-230">Performance and Tuning</span></span>
<span data-ttu-id="71f4a-231">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="71f4a-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
