---
title: "aaaMove danych z programu MySQL przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z programu MySQL bazy danych przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="dd998-103">Przenoszenie danych z MySQL przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="dd998-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="dd998-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd998-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="dd998-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dd998-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="dd998-106">Można skopiować danych z lokalnego MySQL magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="dd998-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="dd998-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="dd998-108">Fabryka danych aktualnie obsługuje tylko przeniesienie tooother magazyny danych magazynu danych z danych MySQL, ale nie do przenoszenia danych z magazynu magazynów danych MySQL tooan innych danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dd998-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dd998-109">Prerequisites</span></span>
<span data-ttu-id="dd998-110">Usługi fabryka danych obsługuje łączenia źródeł MySQL tooon lokalnych przy użyciu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="dd998-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="dd998-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="dd998-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="dd998-112">Nawet wtedy, gdy baza danych MySQL hello znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama.</span><span class="sxs-lookup"><span data-stu-id="dd998-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="dd998-113">Możesz zainstalować bramę hello na powitania tej samej maszyny Wirtualnej jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="dd998-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="dd998-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="dd998-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="dd998-115">Supported versions and installation</span></span>
<span data-ttu-id="dd998-116">Dla bramy zarządzania danymi tooconnect toohello baza danych MySQL, potrzebujesz tooinstall hello [MySQL Connector/Net systemu Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (wersja 6.6.5 lub nowszej) na takie same hello systemu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="dd998-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="dd998-117">MySQL w wersji 5.1 i nowszych jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="dd998-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="dd998-118">Jeśli naciśniesz błąd "Uwierzytelnianie nie powiodło się, ponieważ strona zdalna hello zamknęła hello transportu strumienia.", należy wziąć pod uwagę hello tooupgrade MySQL Connector/Net toohigher wersji.</span><span class="sxs-lookup"><span data-stu-id="dd998-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="dd998-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="dd998-119">Getting started</span></span>
<span data-ttu-id="dd998-120">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="dd998-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="dd998-121">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="dd998-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="dd998-122">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="dd998-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="dd998-123">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="dd998-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="dd998-124">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dd998-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="dd998-125">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="dd998-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="dd998-126">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="dd998-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="dd998-127">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dd998-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="dd998-128">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="dd998-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="dd998-129">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="dd998-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="dd998-130">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="dd998-131">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego magazynu danych MySQL, zobacz [przykład JSON: kopiowanie danych z MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="dd998-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="dd998-132">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych MySQL tooa określonych jednostek fabryki danych używanych toodefine:</span><span class="sxs-lookup"><span data-stu-id="dd998-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="dd998-133">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="dd998-133">Linked service properties</span></span>
<span data-ttu-id="dd998-134">Hello w poniższej tabeli przedstawiono opis usługi określonego tooMySQL połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="dd998-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="dd998-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dd998-135">Property</span></span> | <span data-ttu-id="dd998-136">Opis</span><span class="sxs-lookup"><span data-stu-id="dd998-136">Description</span></span> | <span data-ttu-id="dd998-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd998-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd998-138">type</span><span class="sxs-lookup"><span data-stu-id="dd998-138">type</span></span> |<span data-ttu-id="dd998-139">musi mieć ustawioną właściwość type Hello: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="dd998-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="dd998-140">Tak</span><span class="sxs-lookup"><span data-stu-id="dd998-140">Yes</span></span> |
| <span data-ttu-id="dd998-141">serwer</span><span class="sxs-lookup"><span data-stu-id="dd998-141">server</span></span> |<span data-ttu-id="dd998-142">Nazwa serwera MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="dd998-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="dd998-143">Tak</span><span class="sxs-lookup"><span data-stu-id="dd998-143">Yes</span></span> |
| <span data-ttu-id="dd998-144">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="dd998-144">database</span></span> |<span data-ttu-id="dd998-145">Nazwa bazy danych MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="dd998-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="dd998-146">Tak</span><span class="sxs-lookup"><span data-stu-id="dd998-146">Yes</span></span> |
| <span data-ttu-id="dd998-147">Schemat</span><span class="sxs-lookup"><span data-stu-id="dd998-147">schema</span></span> |<span data-ttu-id="dd998-148">Nazwa schematu hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="dd998-149">Nie</span><span class="sxs-lookup"><span data-stu-id="dd998-149">No</span></span> |
| <span data-ttu-id="dd998-150">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="dd998-150">authenticationType</span></span> |<span data-ttu-id="dd998-151">Typ uwierzytelniania używany toohello tooconnect baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd998-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="dd998-152">Możliwe wartości to: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="dd998-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="dd998-153">Tak</span><span class="sxs-lookup"><span data-stu-id="dd998-153">Yes</span></span> |
| <span data-ttu-id="dd998-154">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="dd998-154">username</span></span> |<span data-ttu-id="dd998-155">Określ bazy danych MySQL toohello tooconnect nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dd998-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="dd998-156">Tak</span><span class="sxs-lookup"><span data-stu-id="dd998-156">Yes</span></span> |
| <span data-ttu-id="dd998-157">hasło</span><span class="sxs-lookup"><span data-stu-id="dd998-157">password</span></span> |<span data-ttu-id="dd998-158">Określ hasło dla konta użytkownika hello określona.</span><span class="sxs-lookup"><span data-stu-id="dd998-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="dd998-159">Tak</span><span class="sxs-lookup"><span data-stu-id="dd998-159">Yes</span></span> |
| <span data-ttu-id="dd998-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="dd998-160">gatewayName</span></span> |<span data-ttu-id="dd998-161">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd998-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="dd998-162">Tak</span><span class="sxs-lookup"><span data-stu-id="dd998-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="dd998-163">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="dd998-163">Dataset properties</span></span>
<span data-ttu-id="dd998-164">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="dd998-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="dd998-165">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="dd998-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="dd998-166">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="dd998-167">Witaj typeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych MySQL) ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="dd998-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="dd998-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dd998-168">Property</span></span> | <span data-ttu-id="dd998-169">Opis</span><span class="sxs-lookup"><span data-stu-id="dd998-169">Description</span></span> | <span data-ttu-id="dd998-170">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd998-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd998-171">tableName</span><span class="sxs-lookup"><span data-stu-id="dd998-171">tableName</span></span> |<span data-ttu-id="dd998-172">Nazwa tabeli hello w hello wystąpienie bazy danych MySQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="dd998-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="dd998-173">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="dd998-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="dd998-174">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="dd998-174">Copy activity properties</span></span>
<span data-ttu-id="dd998-175">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="dd998-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="dd998-176">Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="dd998-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="dd998-177">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="dd998-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="dd998-178">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="dd998-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="dd998-179">Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje MySQL), hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="dd998-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="dd998-180">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dd998-180">Property</span></span> | <span data-ttu-id="dd998-181">Opis</span><span class="sxs-lookup"><span data-stu-id="dd998-181">Description</span></span> | <span data-ttu-id="dd998-182">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="dd998-182">Allowed values</span></span> | <span data-ttu-id="dd998-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd998-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dd998-184">query</span><span class="sxs-lookup"><span data-stu-id="dd998-184">query</span></span> |<span data-ttu-id="dd998-185">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="dd998-186">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="dd998-186">SQL query string.</span></span> <span data-ttu-id="dd998-187">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="dd998-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="dd998-188">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="dd998-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="dd998-189">Przykład JSON: kopiowanie danych z tooAzure MySQL obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="dd998-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="dd998-190">W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dd998-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="dd998-191">Pokazuje, jak toocopy danych z programu MySQL lokalnej bazy danych tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dd998-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="dd998-192">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="dd998-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd998-193">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="dd998-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="dd998-194">Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="dd998-195">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="dd998-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="dd998-196">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="dd998-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="dd998-197">Połączonej usługi typu [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dd998-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="dd998-198">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dd998-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="dd998-199">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd998-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="dd998-200">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd998-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="dd998-201">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dd998-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="dd998-202">przykład Witaj co godzinę kopiuje dane z wyniku kwerendy w obiekcie blob tooa bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd998-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="dd998-203">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="dd998-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="dd998-204">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="dd998-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="dd998-205">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="dd998-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="dd998-206">**MySQL połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="dd998-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="dd998-207">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd998-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="dd998-208">**Wejściowy zestaw danych MySQL:**</span><span class="sxs-lookup"><span data-stu-id="dd998-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="dd998-209">przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" MySQL i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="dd998-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="dd998-210">Ustawienie "external": "prawda" informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="dd998-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="dd998-211">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="dd998-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="dd998-212">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="dd998-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="dd998-213">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="dd998-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="dd998-214">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="dd998-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="dd998-215">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="dd998-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="dd998-216">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="dd998-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="dd998-217">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="dd998-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="dd998-218">Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="dd998-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="dd998-219">Mapowanie typu dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="dd998-219">Type mapping for MySQL</span></span>
<span data-ttu-id="dd998-220">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:</span><span class="sxs-lookup"><span data-stu-id="dd998-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="dd998-221">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="dd998-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="dd998-222">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="dd998-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="dd998-223">Podczas przenoszenia danych tooMySQL, hello następujące mapowania są używane z typów too.NET typy MySQL.</span><span class="sxs-lookup"><span data-stu-id="dd998-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="dd998-224">Typ bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="dd998-224">MySQL Database type</span></span> | <span data-ttu-id="dd998-225">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="dd998-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="dd998-226">bigint bez znaku</span><span class="sxs-lookup"><span data-stu-id="dd998-226">bigint unsigned</span></span> |<span data-ttu-id="dd998-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="dd998-227">Decimal</span></span> |
| <span data-ttu-id="dd998-228">bigint</span><span class="sxs-lookup"><span data-stu-id="dd998-228">bigint</span></span> |<span data-ttu-id="dd998-229">Int64</span><span class="sxs-lookup"><span data-stu-id="dd998-229">Int64</span></span> |
| <span data-ttu-id="dd998-230">bitowe</span><span class="sxs-lookup"><span data-stu-id="dd998-230">bit</span></span> |<span data-ttu-id="dd998-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="dd998-231">Decimal</span></span> |
| <span data-ttu-id="dd998-232">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="dd998-232">blob</span></span> |<span data-ttu-id="dd998-233">Byte]</span><span class="sxs-lookup"><span data-stu-id="dd998-233">Byte[]</span></span> |
| <span data-ttu-id="dd998-234">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="dd998-234">bool</span></span> |<span data-ttu-id="dd998-235">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="dd998-235">Boolean</span></span> |
| <span data-ttu-id="dd998-236">char</span><span class="sxs-lookup"><span data-stu-id="dd998-236">char</span></span> |<span data-ttu-id="dd998-237">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-237">String</span></span> |
| <span data-ttu-id="dd998-238">Data</span><span class="sxs-lookup"><span data-stu-id="dd998-238">date</span></span> |<span data-ttu-id="dd998-239">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="dd998-239">Datetime</span></span> |
| <span data-ttu-id="dd998-240">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="dd998-240">datetime</span></span> |<span data-ttu-id="dd998-241">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="dd998-241">Datetime</span></span> |
| <span data-ttu-id="dd998-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="dd998-242">decimal</span></span> |<span data-ttu-id="dd998-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="dd998-243">Decimal</span></span> |
| <span data-ttu-id="dd998-244">podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="dd998-244">double precision</span></span> |<span data-ttu-id="dd998-245">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="dd998-245">Double</span></span> |
| <span data-ttu-id="dd998-246">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="dd998-246">double</span></span> |<span data-ttu-id="dd998-247">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="dd998-247">Double</span></span> |
| <span data-ttu-id="dd998-248">wyliczenia</span><span class="sxs-lookup"><span data-stu-id="dd998-248">enum</span></span> |<span data-ttu-id="dd998-249">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-249">String</span></span> |
| <span data-ttu-id="dd998-250">Float</span><span class="sxs-lookup"><span data-stu-id="dd998-250">float</span></span> |<span data-ttu-id="dd998-251">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="dd998-251">Single</span></span> |
| <span data-ttu-id="dd998-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="dd998-252">int unsigned</span></span> |<span data-ttu-id="dd998-253">Int64</span><span class="sxs-lookup"><span data-stu-id="dd998-253">Int64</span></span> |
| <span data-ttu-id="dd998-254">int</span><span class="sxs-lookup"><span data-stu-id="dd998-254">int</span></span> |<span data-ttu-id="dd998-255">Int32</span><span class="sxs-lookup"><span data-stu-id="dd998-255">Int32</span></span> |
| <span data-ttu-id="dd998-256">Liczba całkowita bez znaku</span><span class="sxs-lookup"><span data-stu-id="dd998-256">integer unsigned</span></span> |<span data-ttu-id="dd998-257">Int64</span><span class="sxs-lookup"><span data-stu-id="dd998-257">Int64</span></span> |
| <span data-ttu-id="dd998-258">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="dd998-258">integer</span></span> |<span data-ttu-id="dd998-259">Int32</span><span class="sxs-lookup"><span data-stu-id="dd998-259">Int32</span></span> |
| <span data-ttu-id="dd998-260">długie varbinary</span><span class="sxs-lookup"><span data-stu-id="dd998-260">long varbinary</span></span> |<span data-ttu-id="dd998-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="dd998-261">Byte[]</span></span> |
| <span data-ttu-id="dd998-262">varchar długa</span><span class="sxs-lookup"><span data-stu-id="dd998-262">long varchar</span></span> |<span data-ttu-id="dd998-263">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-263">String</span></span> |
| <span data-ttu-id="dd998-264">longblob</span><span class="sxs-lookup"><span data-stu-id="dd998-264">longblob</span></span> |<span data-ttu-id="dd998-265">Byte]</span><span class="sxs-lookup"><span data-stu-id="dd998-265">Byte[]</span></span> |
| <span data-ttu-id="dd998-266">LONGTEXT</span><span class="sxs-lookup"><span data-stu-id="dd998-266">longtext</span></span> |<span data-ttu-id="dd998-267">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-267">String</span></span> |
| <span data-ttu-id="dd998-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="dd998-268">mediumblob</span></span> |<span data-ttu-id="dd998-269">Byte]</span><span class="sxs-lookup"><span data-stu-id="dd998-269">Byte[]</span></span> |
| <span data-ttu-id="dd998-270">mediumint bez znaku</span><span class="sxs-lookup"><span data-stu-id="dd998-270">mediumint unsigned</span></span> |<span data-ttu-id="dd998-271">Int64</span><span class="sxs-lookup"><span data-stu-id="dd998-271">Int64</span></span> |
| <span data-ttu-id="dd998-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="dd998-272">mediumint</span></span> |<span data-ttu-id="dd998-273">Int32</span><span class="sxs-lookup"><span data-stu-id="dd998-273">Int32</span></span> |
| <span data-ttu-id="dd998-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="dd998-274">mediumtext</span></span> |<span data-ttu-id="dd998-275">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-275">String</span></span> |
| <span data-ttu-id="dd998-276">numeryczne</span><span class="sxs-lookup"><span data-stu-id="dd998-276">numeric</span></span> |<span data-ttu-id="dd998-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="dd998-277">Decimal</span></span> |
| <span data-ttu-id="dd998-278">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="dd998-278">real</span></span> |<span data-ttu-id="dd998-279">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="dd998-279">Double</span></span> |
| <span data-ttu-id="dd998-280">zestaw</span><span class="sxs-lookup"><span data-stu-id="dd998-280">set</span></span> |<span data-ttu-id="dd998-281">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-281">String</span></span> |
| <span data-ttu-id="dd998-282">smallint bez znaku</span><span class="sxs-lookup"><span data-stu-id="dd998-282">smallint unsigned</span></span> |<span data-ttu-id="dd998-283">Int32</span><span class="sxs-lookup"><span data-stu-id="dd998-283">Int32</span></span> |
| <span data-ttu-id="dd998-284">smallint</span><span class="sxs-lookup"><span data-stu-id="dd998-284">smallint</span></span> |<span data-ttu-id="dd998-285">Int16</span><span class="sxs-lookup"><span data-stu-id="dd998-285">Int16</span></span> |
| <span data-ttu-id="dd998-286">Tekst</span><span class="sxs-lookup"><span data-stu-id="dd998-286">text</span></span> |<span data-ttu-id="dd998-287">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-287">String</span></span> |
| <span data-ttu-id="dd998-288">time</span><span class="sxs-lookup"><span data-stu-id="dd998-288">time</span></span> |<span data-ttu-id="dd998-289">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="dd998-289">TimeSpan</span></span> |
| <span data-ttu-id="dd998-290">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="dd998-290">timestamp</span></span> |<span data-ttu-id="dd998-291">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="dd998-291">Datetime</span></span> |
| <span data-ttu-id="dd998-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="dd998-292">tinyblob</span></span> |<span data-ttu-id="dd998-293">Byte]</span><span class="sxs-lookup"><span data-stu-id="dd998-293">Byte[]</span></span> |
| <span data-ttu-id="dd998-294">tinyint bez znaku</span><span class="sxs-lookup"><span data-stu-id="dd998-294">tinyint unsigned</span></span> |<span data-ttu-id="dd998-295">Int16</span><span class="sxs-lookup"><span data-stu-id="dd998-295">Int16</span></span> |
| <span data-ttu-id="dd998-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="dd998-296">tinyint</span></span> |<span data-ttu-id="dd998-297">Int16</span><span class="sxs-lookup"><span data-stu-id="dd998-297">Int16</span></span> |
| <span data-ttu-id="dd998-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="dd998-298">tinytext</span></span> |<span data-ttu-id="dd998-299">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-299">String</span></span> |
| <span data-ttu-id="dd998-300">varchar</span><span class="sxs-lookup"><span data-stu-id="dd998-300">varchar</span></span> |<span data-ttu-id="dd998-301">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dd998-301">String</span></span> |
| <span data-ttu-id="dd998-302">Roku</span><span class="sxs-lookup"><span data-stu-id="dd998-302">year</span></span> |<span data-ttu-id="dd998-303">int</span><span class="sxs-lookup"><span data-stu-id="dd998-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="dd998-304">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="dd998-304">Map source toosink columns</span></span>
<span data-ttu-id="dd998-305">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="dd998-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="dd998-306">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="dd998-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="dd998-307">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="dd998-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="dd998-308">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="dd998-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="dd998-309">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="dd998-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="dd998-310">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="dd998-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="dd998-311">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="dd998-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="dd998-312">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="dd998-312">Performance and Tuning</span></span>
<span data-ttu-id="dd998-313">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="dd998-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
