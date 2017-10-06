---
title: "aaaMove danych z programu Teradata przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat łącznika programu Teradata dla hello usługi fabryka danych, które umożliwia przenoszenie danych z bazy danych programu Teradata"
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
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="89430-103">Przenoszenia danych z programu Teradata przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="89430-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="89430-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="89430-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="89430-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="89430-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="89430-106">Można skopiować danych z lokalnego Teradata magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="89430-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="89430-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="89430-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="89430-108">Fabryka danych aktualnie obsługuje tylko przeniesienie tooother magazyny danych magazynu danych ze źródła danych programu Teradata, ale nie do przenoszenia danych z innym magazynie danych programu Teradata tooa danych magazynów.</span><span class="sxs-lookup"><span data-stu-id="89430-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="89430-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89430-109">Prerequisites</span></span>
<span data-ttu-id="89430-110">Fabryka danych obsługuje łączącego źródła Teradata tooon lokalnego za pośrednictwem hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="89430-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="89430-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="89430-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="89430-112">Wymagana jest brama, nawet jeśli hello Teradata znajduje się w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="89430-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="89430-113">Możesz zainstalować bramę hello na powitania sam maszyn wirtualnych IaaS jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="89430-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="89430-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="89430-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="89430-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="89430-115">Supported versions and installation</span></span>
<span data-ttu-id="89430-116">Dla bazy danych programu Teradata. toohello tooconnect brama zarządzania danymi, trzeba tooinstall hello [dostawcy danych .NET dla programu Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) wersji 14 lub powyżej na hello sam system jako hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="89430-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="89430-117">Teradata wersji 12 i nowszej jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="89430-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="89430-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="89430-118">Getting started</span></span>
<span data-ttu-id="89430-119">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="89430-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="89430-120">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="89430-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="89430-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="89430-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="89430-122">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="89430-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="89430-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="89430-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="89430-124">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="89430-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="89430-125">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="89430-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="89430-126">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="89430-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="89430-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="89430-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="89430-128">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="89430-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="89430-129">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="89430-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="89430-130">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych programu Teradata lokalnych, zobacz [przykład JSON: kopiowanie danych z programu Teradata tooAzure obiektu Blob](#json-example-copy-data-from-teradata-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="89430-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="89430-131">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych programu Teradata tooa określonych jednostek używanych toodefine fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="89430-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="89430-132">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="89430-132">Linked service properties</span></span>
<span data-ttu-id="89430-133">Hello w poniższej tabeli przedstawiono opis usługi określonego tooTeradata połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="89430-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="89430-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="89430-134">Property</span></span> | <span data-ttu-id="89430-135">Opis</span><span class="sxs-lookup"><span data-stu-id="89430-135">Description</span></span> | <span data-ttu-id="89430-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89430-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89430-137">type</span><span class="sxs-lookup"><span data-stu-id="89430-137">type</span></span> |<span data-ttu-id="89430-138">musi mieć ustawioną właściwość type Hello: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="89430-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="89430-139">Tak</span><span class="sxs-lookup"><span data-stu-id="89430-139">Yes</span></span> |
| <span data-ttu-id="89430-140">serwer</span><span class="sxs-lookup"><span data-stu-id="89430-140">server</span></span> |<span data-ttu-id="89430-141">Nazwa serwera programu Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="89430-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="89430-142">Tak</span><span class="sxs-lookup"><span data-stu-id="89430-142">Yes</span></span> |
| <span data-ttu-id="89430-143">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="89430-143">authenticationType</span></span> |<span data-ttu-id="89430-144">Typ uwierzytelniania używany toohello tooconnect bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="89430-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="89430-145">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="89430-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="89430-146">Tak</span><span class="sxs-lookup"><span data-stu-id="89430-146">Yes</span></span> |
| <span data-ttu-id="89430-147">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="89430-147">username</span></span> |<span data-ttu-id="89430-148">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="89430-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="89430-149">Nie</span><span class="sxs-lookup"><span data-stu-id="89430-149">No</span></span> |
| <span data-ttu-id="89430-150">hasło</span><span class="sxs-lookup"><span data-stu-id="89430-150">password</span></span> |<span data-ttu-id="89430-151">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89430-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="89430-152">Nie</span><span class="sxs-lookup"><span data-stu-id="89430-152">No</span></span> |
| <span data-ttu-id="89430-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="89430-153">gatewayName</span></span> |<span data-ttu-id="89430-154">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="89430-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="89430-155">Tak</span><span class="sxs-lookup"><span data-stu-id="89430-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="89430-156">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="89430-156">Dataset properties</span></span>
<span data-ttu-id="89430-157">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="89430-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="89430-158">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="89430-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="89430-159">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="89430-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="89430-160">Obecnie nie ma żadnych właściwości typu, obsługiwane dla zestawu danych programu Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="89430-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="89430-161">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="89430-161">Copy activity properties</span></span>
<span data-ttu-id="89430-162">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="89430-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="89430-163">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="89430-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="89430-164">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="89430-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="89430-165">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="89430-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="89430-166">Gdy źródło hello jest typu **RelationalSource** (która obejmuje Teradata), dostępne są następujące właściwości hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="89430-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="89430-167">Właściwość</span><span class="sxs-lookup"><span data-stu-id="89430-167">Property</span></span> | <span data-ttu-id="89430-168">Opis</span><span class="sxs-lookup"><span data-stu-id="89430-168">Description</span></span> | <span data-ttu-id="89430-169">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="89430-169">Allowed values</span></span> | <span data-ttu-id="89430-170">Wymagane</span><span class="sxs-lookup"><span data-stu-id="89430-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89430-171">query</span><span class="sxs-lookup"><span data-stu-id="89430-171">query</span></span> |<span data-ttu-id="89430-172">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="89430-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="89430-173">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="89430-173">SQL query string.</span></span> <span data-ttu-id="89430-174">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="89430-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="89430-175">Tak</span><span class="sxs-lookup"><span data-stu-id="89430-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="89430-176">Przykład JSON: kopiowanie danych z programu Teradata tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="89430-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="89430-177">Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="89430-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="89430-178">Przedstawiają sposób toocopy danych z programu Teradata tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="89430-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="89430-179">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="89430-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="89430-180">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="89430-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="89430-181">Połączonej usługi typu [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89430-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="89430-182">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89430-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="89430-183">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89430-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="89430-184">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89430-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="89430-185">Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="89430-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="89430-186">przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa bazy danych programu Teradata co godzinę.</span><span class="sxs-lookup"><span data-stu-id="89430-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="89430-187">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="89430-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="89430-188">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="89430-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="89430-189">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="89430-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="89430-190">**Teradata połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="89430-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="89430-191">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="89430-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="89430-192">**Wejściowy zestaw danych programu Teradata:**</span><span class="sxs-lookup"><span data-stu-id="89430-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="89430-193">przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" Teradata i zawiera kolumnę o nazwie "timestamp" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="89430-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="89430-194">Ustawienie "external": true informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="89430-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="89430-195">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="89430-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="89430-196">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="89430-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="89430-197">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="89430-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="89430-198">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="89430-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="89430-199">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="89430-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="89430-200">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="89430-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="89430-201">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="89430-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="89430-202">Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="89430-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="89430-203">Mapowanie typu dla programu Teradata</span><span class="sxs-lookup"><span data-stu-id="89430-203">Type mapping for Teradata</span></span>
<span data-ttu-id="89430-204">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, hello działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="89430-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="89430-205">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="89430-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="89430-206">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="89430-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="89430-207">Podczas przenoszenia danych tooTeradata, hello następujące mapowania są używane z too.NET typu programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="89430-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="89430-208">Typ bazy danych programu Teradata</span><span class="sxs-lookup"><span data-stu-id="89430-208">Teradata Database type</span></span> | <span data-ttu-id="89430-209">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="89430-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="89430-210">char</span><span class="sxs-lookup"><span data-stu-id="89430-210">Char</span></span> |<span data-ttu-id="89430-211">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-211">String</span></span> |
| <span data-ttu-id="89430-212">CLOB</span><span class="sxs-lookup"><span data-stu-id="89430-212">Clob</span></span> |<span data-ttu-id="89430-213">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-213">String</span></span> |
| <span data-ttu-id="89430-214">Grafika</span><span class="sxs-lookup"><span data-stu-id="89430-214">Graphic</span></span> |<span data-ttu-id="89430-215">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-215">String</span></span> |
| <span data-ttu-id="89430-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="89430-216">VarChar</span></span> |<span data-ttu-id="89430-217">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-217">String</span></span> |
| <span data-ttu-id="89430-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="89430-218">VarGraphic</span></span> |<span data-ttu-id="89430-219">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-219">String</span></span> |
| <span data-ttu-id="89430-220">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="89430-220">Blob</span></span> |<span data-ttu-id="89430-221">Byte]</span><span class="sxs-lookup"><span data-stu-id="89430-221">Byte[]</span></span> |
| <span data-ttu-id="89430-222">Bajtów</span><span class="sxs-lookup"><span data-stu-id="89430-222">Byte</span></span> |<span data-ttu-id="89430-223">Byte]</span><span class="sxs-lookup"><span data-stu-id="89430-223">Byte[]</span></span> |
| <span data-ttu-id="89430-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="89430-224">VarByte</span></span> |<span data-ttu-id="89430-225">Byte]</span><span class="sxs-lookup"><span data-stu-id="89430-225">Byte[]</span></span> |
| <span data-ttu-id="89430-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="89430-226">BigInt</span></span> |<span data-ttu-id="89430-227">Int64</span><span class="sxs-lookup"><span data-stu-id="89430-227">Int64</span></span> |
| <span data-ttu-id="89430-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="89430-228">ByteInt</span></span> |<span data-ttu-id="89430-229">Int16</span><span class="sxs-lookup"><span data-stu-id="89430-229">Int16</span></span> |
| <span data-ttu-id="89430-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="89430-230">Decimal</span></span> |<span data-ttu-id="89430-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="89430-231">Decimal</span></span> |
| <span data-ttu-id="89430-232">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="89430-232">Double</span></span> |<span data-ttu-id="89430-233">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="89430-233">Double</span></span> |
| <span data-ttu-id="89430-234">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="89430-234">Integer</span></span> |<span data-ttu-id="89430-235">Int32</span><span class="sxs-lookup"><span data-stu-id="89430-235">Int32</span></span> |
| <span data-ttu-id="89430-236">Liczba</span><span class="sxs-lookup"><span data-stu-id="89430-236">Number</span></span> |<span data-ttu-id="89430-237">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="89430-237">Double</span></span> |
| <span data-ttu-id="89430-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="89430-238">SmallInt</span></span> |<span data-ttu-id="89430-239">Int16</span><span class="sxs-lookup"><span data-stu-id="89430-239">Int16</span></span> |
| <span data-ttu-id="89430-240">Date</span><span class="sxs-lookup"><span data-stu-id="89430-240">Date</span></span> |<span data-ttu-id="89430-241">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="89430-241">DateTime</span></span> |
| <span data-ttu-id="89430-242">Time</span><span class="sxs-lookup"><span data-stu-id="89430-242">Time</span></span> |<span data-ttu-id="89430-243">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-243">TimeSpan</span></span> |
| <span data-ttu-id="89430-244">Czas ze strefą czasową</span><span class="sxs-lookup"><span data-stu-id="89430-244">Time With Time Zone</span></span> |<span data-ttu-id="89430-245">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-245">String</span></span> |
| <span data-ttu-id="89430-246">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="89430-246">Timestamp</span></span> |<span data-ttu-id="89430-247">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="89430-247">DateTime</span></span> |
| <span data-ttu-id="89430-248">Sygnatura czasowa ze strefą czasową</span><span class="sxs-lookup"><span data-stu-id="89430-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="89430-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="89430-249">DateTimeOffset</span></span> |
| <span data-ttu-id="89430-250">Interwał dnia</span><span class="sxs-lookup"><span data-stu-id="89430-250">Interval Day</span></span> |<span data-ttu-id="89430-251">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-251">TimeSpan</span></span> |
| <span data-ttu-id="89430-252">Interwał tooHour dnia</span><span class="sxs-lookup"><span data-stu-id="89430-252">Interval Day tooHour</span></span> |<span data-ttu-id="89430-253">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-253">TimeSpan</span></span> |
| <span data-ttu-id="89430-254">Interwał tooMinute dnia</span><span class="sxs-lookup"><span data-stu-id="89430-254">Interval Day tooMinute</span></span> |<span data-ttu-id="89430-255">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-255">TimeSpan</span></span> |
| <span data-ttu-id="89430-256">Interwał tooSecond dnia</span><span class="sxs-lookup"><span data-stu-id="89430-256">Interval Day tooSecond</span></span> |<span data-ttu-id="89430-257">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-257">TimeSpan</span></span> |
| <span data-ttu-id="89430-258">Interwał, godzinę</span><span class="sxs-lookup"><span data-stu-id="89430-258">Interval Hour</span></span> |<span data-ttu-id="89430-259">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-259">TimeSpan</span></span> |
| <span data-ttu-id="89430-260">Interwał tooMinute godzinę</span><span class="sxs-lookup"><span data-stu-id="89430-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="89430-261">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-261">TimeSpan</span></span> |
| <span data-ttu-id="89430-262">Interwał tooSecond godzinę</span><span class="sxs-lookup"><span data-stu-id="89430-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="89430-263">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-263">TimeSpan</span></span> |
| <span data-ttu-id="89430-264">Interwał minutę</span><span class="sxs-lookup"><span data-stu-id="89430-264">Interval Minute</span></span> |<span data-ttu-id="89430-265">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-265">TimeSpan</span></span> |
| <span data-ttu-id="89430-266">Interwał tooSecond minuty</span><span class="sxs-lookup"><span data-stu-id="89430-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="89430-267">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-267">TimeSpan</span></span> |
| <span data-ttu-id="89430-268">Interwał drugi</span><span class="sxs-lookup"><span data-stu-id="89430-268">Interval Second</span></span> |<span data-ttu-id="89430-269">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="89430-269">TimeSpan</span></span> |
| <span data-ttu-id="89430-270">Interwał roku</span><span class="sxs-lookup"><span data-stu-id="89430-270">Interval Year</span></span> |<span data-ttu-id="89430-271">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-271">String</span></span> |
| <span data-ttu-id="89430-272">Interwał tooMonth roku</span><span class="sxs-lookup"><span data-stu-id="89430-272">Interval Year tooMonth</span></span> |<span data-ttu-id="89430-273">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-273">String</span></span> |
| <span data-ttu-id="89430-274">Interwał miesiąca</span><span class="sxs-lookup"><span data-stu-id="89430-274">Interval Month</span></span> |<span data-ttu-id="89430-275">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-275">String</span></span> |
| <span data-ttu-id="89430-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="89430-276">Period(Date)</span></span> |<span data-ttu-id="89430-277">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-277">String</span></span> |
| <span data-ttu-id="89430-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="89430-278">Period(Time)</span></span> |<span data-ttu-id="89430-279">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-279">String</span></span> |
| <span data-ttu-id="89430-280">Okres (czas ze strefą czasową)</span><span class="sxs-lookup"><span data-stu-id="89430-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="89430-281">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-281">String</span></span> |
| <span data-ttu-id="89430-282">Period(TimeStamp)</span><span class="sxs-lookup"><span data-stu-id="89430-282">Period(Timestamp)</span></span> |<span data-ttu-id="89430-283">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-283">String</span></span> |
| <span data-ttu-id="89430-284">Okres (sygnatura ze strefą czasową)</span><span class="sxs-lookup"><span data-stu-id="89430-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="89430-285">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-285">String</span></span> |
| <span data-ttu-id="89430-286">XML</span><span class="sxs-lookup"><span data-stu-id="89430-286">Xml</span></span> |<span data-ttu-id="89430-287">Ciąg</span><span class="sxs-lookup"><span data-stu-id="89430-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="89430-288">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="89430-288">Map source toosink columns</span></span>
<span data-ttu-id="89430-289">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="89430-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="89430-290">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="89430-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="89430-291">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="89430-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="89430-292">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="89430-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="89430-293">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="89430-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="89430-294">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="89430-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="89430-295">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="89430-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="89430-296">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="89430-296">Performance and Tuning</span></span>
<span data-ttu-id="89430-297">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="89430-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
