---
title: "aaaMove danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="adca4-103">Przenoszenie danych z programu SAP Business Warehouse przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="adca4-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="adca4-104">W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z lokalnymi SAP Business magazynu (BW).</span><span class="sxs-lookup"><span data-stu-id="adca4-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="adca4-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="adca4-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="adca4-106">Można skopiować danych z lokalnego SAP Business Warehouse magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="adca4-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="adca4-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="adca4-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="adca4-108">Fabryka danych aktualnie obsługuje tylko do przenoszenia danych z danych tooother SAP Business Warehouse przechowuje, ale nie w przypadku przenoszenia danych z innych danych przechowują tooan SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="adca4-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="adca4-109">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="adca4-109">Supported versions and installation</span></span>
<span data-ttu-id="adca4-110">Ten łącznik obsługuje wersję SAP Business Warehouse 7.x.</span><span class="sxs-lookup"><span data-stu-id="adca4-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="adca4-111">Obsługuje ona kopiowania danych z InfoCubes i QueryCubes (takie jak zapytania BEx) przy użyciu zapytania MDX.</span><span class="sxs-lookup"><span data-stu-id="adca4-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="adca4-112">tooenable hello łączności toohello wystąpienia programu SAP BW zainstalować hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="adca4-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="adca4-113">**Brama zarządzania danymi**: połączenie lokalne tooon danych obsługuje usługi fabryka danych magazynów (w tym SAP Business Warehouse) przy użyciu składnika o nazwie brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="adca4-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="adca4-114">Zobacz toolearn o brama zarządzania danymi i szczegółowe instrukcje dotyczące konfigurowania bramy hello [przenoszenie danych między danymi lokalnymi przechowywany magazyn danych toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="adca4-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="adca4-115">Nawet jeśli hello SAP Business Warehouse znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama.</span><span class="sxs-lookup"><span data-stu-id="adca4-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="adca4-116">Możesz zainstalować bramę hello na powitania tej samej maszyny Wirtualnej jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="adca4-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="adca4-117">**SAP NetWeaver biblioteki** na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="adca4-118">Hello SAP Netweaver biblioteki można uzyskać od administratora SAP, lub bezpośrednio z hello [Centrum pobierania oprogramowania SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="adca4-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="adca4-119">Wyszukaj hello **&#1025361; Uwaga SAP** lokalizację pobierania hello tooget hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="adca4-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="adca4-120">Upewnij się, że architektura hello hello SAP NetWeaver biblioteki (32-bitowy lub 64-bitowy) odpowiada instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="adca4-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="adca4-121">Następnie zainstaluj wszystkie pliki zawarte w hello SAP NetWeaver RFC SDK zgodnie z toohello Uwaga SAP.</span><span class="sxs-lookup"><span data-stu-id="adca4-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="adca4-122">Witaj SAP NetWeaver biblioteki dołączony jest również hello instalacji narzędzi klienta SAP.</span><span class="sxs-lookup"><span data-stu-id="adca4-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="adca4-123">Umieść biblioteki DLL hello wyodrębniony z hello NetWeaver RFC SDK w folderze system32.</span><span class="sxs-lookup"><span data-stu-id="adca4-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="adca4-124">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="adca4-124">Getting started</span></span>
<span data-ttu-id="adca4-125">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="adca4-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="adca4-126">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="adca4-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="adca4-127">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="adca4-128">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="adca4-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="adca4-129">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="adca4-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="adca4-130">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="adca4-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="adca4-131">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="adca4-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="adca4-132">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="adca4-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="adca4-133">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="adca4-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="adca4-134">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="adca4-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="adca4-135">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="adca4-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="adca4-136">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego SAP Business Warehouse, zobacz [przykład JSON: kopiowanie danych z programu SAP Business Warehouse tooAzure obiektu Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="adca4-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="adca4-137">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych programu SAP BW tooan określonych jednostek fabryki danych używanych toodefine:</span><span class="sxs-lookup"><span data-stu-id="adca4-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="adca4-138">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="adca4-138">Linked service properties</span></span>
<span data-ttu-id="adca4-139">Witaj w poniższej tabeli przedstawiono opis dla określonych tooSAP elementów JSON usługi biznesowe magazynu (BW) połączony.</span><span class="sxs-lookup"><span data-stu-id="adca4-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="adca4-140">Właściwość</span><span class="sxs-lookup"><span data-stu-id="adca4-140">Property</span></span> | <span data-ttu-id="adca4-141">Opis</span><span class="sxs-lookup"><span data-stu-id="adca4-141">Description</span></span> | <span data-ttu-id="adca4-142">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="adca4-142">Allowed values</span></span> | <span data-ttu-id="adca4-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="adca4-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="adca4-144">serwer</span><span class="sxs-lookup"><span data-stu-id="adca4-144">server</span></span> | <span data-ttu-id="adca4-145">Nazwa serwera hello, na które hello programu SAP BW znajduje się wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="adca4-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="adca4-146">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-146">string</span></span> | <span data-ttu-id="adca4-147">Tak</span><span class="sxs-lookup"><span data-stu-id="adca4-147">Yes</span></span>
<span data-ttu-id="adca4-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="adca4-148">systemNumber</span></span> | <span data-ttu-id="adca4-149">Numer systemu hello systemu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="adca4-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="adca4-150">Liczba dziesiętna dwucyfrowe reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="adca4-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="adca4-151">Tak</span><span class="sxs-lookup"><span data-stu-id="adca4-151">Yes</span></span>
<span data-ttu-id="adca4-152">clientId</span><span class="sxs-lookup"><span data-stu-id="adca4-152">clientId</span></span> | <span data-ttu-id="adca4-153">Identyfikator klienta na powitania klienta w hello systemu SAP W.</span><span class="sxs-lookup"><span data-stu-id="adca4-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="adca4-154">Trzycyfrowa liczba dziesiętna reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="adca4-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="adca4-155">Tak</span><span class="sxs-lookup"><span data-stu-id="adca4-155">Yes</span></span>
<span data-ttu-id="adca4-156">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="adca4-156">username</span></span> | <span data-ttu-id="adca4-157">Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera</span><span class="sxs-lookup"><span data-stu-id="adca4-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="adca4-158">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-158">string</span></span> | <span data-ttu-id="adca4-159">Tak</span><span class="sxs-lookup"><span data-stu-id="adca4-159">Yes</span></span>
<span data-ttu-id="adca4-160">hasło</span><span class="sxs-lookup"><span data-stu-id="adca4-160">password</span></span> | <span data-ttu-id="adca4-161">Hasło dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-161">Password for hello user.</span></span> | <span data-ttu-id="adca4-162">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-162">string</span></span> | <span data-ttu-id="adca4-163">Tak</span><span class="sxs-lookup"><span data-stu-id="adca4-163">Yes</span></span>
<span data-ttu-id="adca4-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="adca4-164">gatewayName</span></span> | <span data-ttu-id="adca4-165">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego programu SAP BW wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="adca4-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="adca4-166">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-166">string</span></span> | <span data-ttu-id="adca4-167">Tak</span><span class="sxs-lookup"><span data-stu-id="adca4-167">Yes</span></span>
<span data-ttu-id="adca4-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="adca4-168">encryptedCredential</span></span> | <span data-ttu-id="adca4-169">Witaj zaszyfrowanego ciągu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="adca4-169">hello encrypted credential string.</span></span> | <span data-ttu-id="adca4-170">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-170">string</span></span> | <span data-ttu-id="adca4-171">Nie</span><span class="sxs-lookup"><span data-stu-id="adca4-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="adca4-172">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="adca4-172">Dataset properties</span></span>
<span data-ttu-id="adca4-173">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="adca4-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="adca4-174">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="adca4-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="adca4-175">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="adca4-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="adca4-176">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych z programu SAP BW hello typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="adca4-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="adca4-177">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="adca4-177">Copy activity properties</span></span>
<span data-ttu-id="adca4-178">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="adca4-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="adca4-179">Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="adca4-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="adca4-180">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="adca4-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="adca4-181">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="adca4-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="adca4-182">Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje programu SAP BW), hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="adca4-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="adca4-183">Właściwość</span><span class="sxs-lookup"><span data-stu-id="adca4-183">Property</span></span> | <span data-ttu-id="adca4-184">Opis</span><span class="sxs-lookup"><span data-stu-id="adca4-184">Description</span></span> | <span data-ttu-id="adca4-185">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="adca4-185">Allowed values</span></span> | <span data-ttu-id="adca4-186">Wymagane</span><span class="sxs-lookup"><span data-stu-id="adca4-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="adca4-187">query</span><span class="sxs-lookup"><span data-stu-id="adca4-187">query</span></span> | <span data-ttu-id="adca4-188">Określa dane tooread zapytania MDX hello z wystąpienia programu SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="adca4-189">Zapytania MDX.</span><span class="sxs-lookup"><span data-stu-id="adca4-189">MDX query.</span></span> | <span data-ttu-id="adca4-190">Tak</span><span class="sxs-lookup"><span data-stu-id="adca4-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="adca4-191">Przykład JSON: kopiowanie danych z programu SAP Business Warehouse tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="adca4-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="adca4-192">Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="adca4-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="adca4-193">W tym przykładzie pokazano sposób toocopy danych z lokalnego SAP Business Warehouse tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="adca4-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="adca4-194">Jednak dane mogą być kopiowane **bezpośrednio** tooany wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="adca4-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="adca4-195">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="adca4-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="adca4-196">Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="adca4-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="adca4-197">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="adca4-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="adca4-198">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="adca4-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="adca4-199">Połączonej usługi typu [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="adca4-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="adca4-200">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="adca4-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="adca4-201">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="adca4-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="adca4-202">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="adca4-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="adca4-203">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="adca4-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="adca4-204">Przykładowe Hello co godzinę kopiuje dane z programu SAP Business Warehouse tooan wystąpienia obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="adca4-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="adca4-205">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="adca4-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="adca4-206">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="adca4-207">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="adca4-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="adca4-208">SAP Business Warehouse połączona usługa</span><span class="sxs-lookup"><span data-stu-id="adca4-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="adca4-209">To połączone usługi łączy fabrykę danych toohello wystąpienia programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="adca4-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="adca4-210">Właściwość type Hello ustawiono zbyt**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="adca4-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="adca4-211">Witaj typeProperties sekcja zawiera informacje o połączeniu dla wystąpienia programu SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="adca4-212">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="adca4-212">Azure Storage linked service</span></span>
<span data-ttu-id="adca4-213">To połączone usługi łączy fabrykę danych toohello konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="adca4-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="adca4-214">Właściwość type Hello ustawiono zbyt**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="adca4-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="adca4-215">Witaj typeProperties sekcja zawiera informacje o połączeniu dla hello konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="adca4-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="adca4-216">Wejściowy zestaw danych SAP BW</span><span class="sxs-lookup"><span data-stu-id="adca4-216">SAP BW input dataset</span></span>
<span data-ttu-id="adca4-217">Ten zestaw danych definiuje zestaw danych SAP Business Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="adca4-218">Zbyt Ustaw typ hello DataSet fabryki danych hello**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="adca4-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="adca4-219">Obecnie nie określisz żadnych właściwości określonego typu dla programu SAP BW zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="adca4-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="adca4-220">zapytania Hello w definicji działania kopiowania hello Określa, jakie tooread danych z wystąpienia programu SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="adca4-221">Ustawienie właściwości external tootrue informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="adca4-222">Częstotliwość i interwał właściwości definiuje hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="adca4-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="adca4-223">W takim przypadku hello dane są odczytywane z wystąpienia programu SAP BW hello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="adca4-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="adca4-224">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="adca4-224">Azure Blob output dataset</span></span>
<span data-ttu-id="adca4-225">Ten zestaw danych definiuje hello wyjściowego obiektu Blob systemu Azure zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="adca4-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="adca4-226">ustawiono tooAzureBlob Hello typu właściwości.</span><span class="sxs-lookup"><span data-stu-id="adca4-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="adca4-227">sekcja typeProperties Hello zawiera, którym są przechowywane dane hello skopiowane z wystąpienia programu SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="adca4-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="adca4-228">Hello są zapisywane dane nowego obiektu blob tooa co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="adca4-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="adca4-229">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="adca4-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="adca4-230">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="adca4-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="adca4-231">W potoku z działanie kopiowania</span><span class="sxs-lookup"><span data-stu-id="adca4-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="adca4-232">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="adca4-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="adca4-233">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** (dla programu SAP BW źródła) i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="adca4-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="adca4-234">Zapytanie Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="adca4-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="adca4-235">Mapowanie typu dla programu SAP BW</span><span class="sxs-lookup"><span data-stu-id="adca4-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="adca4-236">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:</span><span class="sxs-lookup"><span data-stu-id="adca4-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="adca4-237">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="adca4-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="adca4-238">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="adca4-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="adca4-239">Podczas przenoszenia danych z programu SAP BW, następujące mapowania hello są używane z programu SAP BW typy too.NET typów.</span><span class="sxs-lookup"><span data-stu-id="adca4-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="adca4-240">Typ danych w hello ABAP słownik</span><span class="sxs-lookup"><span data-stu-id="adca4-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="adca4-241">Typ danych .net</span><span class="sxs-lookup"><span data-stu-id="adca4-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="adca4-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="adca4-242">ACCP</span></span> |  <span data-ttu-id="adca4-243">int</span><span class="sxs-lookup"><span data-stu-id="adca4-243">Int</span></span>
<span data-ttu-id="adca4-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="adca4-244">CHAR</span></span> | <span data-ttu-id="adca4-245">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-245">String</span></span>
<span data-ttu-id="adca4-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="adca4-246">CLNT</span></span> | <span data-ttu-id="adca4-247">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-247">String</span></span>
<span data-ttu-id="adca4-248">BI</span><span class="sxs-lookup"><span data-stu-id="adca4-248">CURR</span></span> | <span data-ttu-id="adca4-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="adca4-249">Decimal</span></span>
<span data-ttu-id="adca4-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="adca4-250">CUKY</span></span> | <span data-ttu-id="adca4-251">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-251">String</span></span>
<span data-ttu-id="adca4-252">DEC</span><span class="sxs-lookup"><span data-stu-id="adca4-252">DEC</span></span> | <span data-ttu-id="adca4-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="adca4-253">Decimal</span></span>
<span data-ttu-id="adca4-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="adca4-254">FLTP</span></span> | <span data-ttu-id="adca4-255">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="adca4-255">Double</span></span>
<span data-ttu-id="adca4-256">INT1</span><span class="sxs-lookup"><span data-stu-id="adca4-256">INT1</span></span> | <span data-ttu-id="adca4-257">Bajtów</span><span class="sxs-lookup"><span data-stu-id="adca4-257">Byte</span></span>
<span data-ttu-id="adca4-258">INT2</span><span class="sxs-lookup"><span data-stu-id="adca4-258">INT2</span></span> | <span data-ttu-id="adca4-259">Int16</span><span class="sxs-lookup"><span data-stu-id="adca4-259">Int16</span></span>
<span data-ttu-id="adca4-260">INT4</span><span class="sxs-lookup"><span data-stu-id="adca4-260">INT4</span></span> | <span data-ttu-id="adca4-261">int</span><span class="sxs-lookup"><span data-stu-id="adca4-261">Int</span></span>
<span data-ttu-id="adca4-262">JĘZYK</span><span class="sxs-lookup"><span data-stu-id="adca4-262">LANG</span></span> | <span data-ttu-id="adca4-263">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-263">String</span></span>
<span data-ttu-id="adca4-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="adca4-264">LCHR</span></span> | <span data-ttu-id="adca4-265">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-265">String</span></span>
<span data-ttu-id="adca4-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="adca4-266">LRAW</span></span> | <span data-ttu-id="adca4-267">Byte]</span><span class="sxs-lookup"><span data-stu-id="adca4-267">Byte[]</span></span>
<span data-ttu-id="adca4-268">PREC</span><span class="sxs-lookup"><span data-stu-id="adca4-268">PREC</span></span> | <span data-ttu-id="adca4-269">Int16</span><span class="sxs-lookup"><span data-stu-id="adca4-269">Int16</span></span>
<span data-ttu-id="adca4-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="adca4-270">QUAN</span></span> | <span data-ttu-id="adca4-271">Decimal</span><span class="sxs-lookup"><span data-stu-id="adca4-271">Decimal</span></span>
<span data-ttu-id="adca4-272">NIEPRZETWORZONE</span><span class="sxs-lookup"><span data-stu-id="adca4-272">RAW</span></span> | <span data-ttu-id="adca4-273">Byte]</span><span class="sxs-lookup"><span data-stu-id="adca4-273">Byte[]</span></span>
<span data-ttu-id="adca4-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="adca4-274">RAWSTRING</span></span> | <span data-ttu-id="adca4-275">Byte]</span><span class="sxs-lookup"><span data-stu-id="adca4-275">Byte[]</span></span>
<span data-ttu-id="adca4-276">CIĄG</span><span class="sxs-lookup"><span data-stu-id="adca4-276">STRING</span></span> | <span data-ttu-id="adca4-277">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-277">String</span></span>
<span data-ttu-id="adca4-278">JEDNOSTKI</span><span class="sxs-lookup"><span data-stu-id="adca4-278">UNIT</span></span> | <span data-ttu-id="adca4-279">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-279">String</span></span>
<span data-ttu-id="adca4-280">DATS</span><span class="sxs-lookup"><span data-stu-id="adca4-280">DATS</span></span> | <span data-ttu-id="adca4-281">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-281">String</span></span>
<span data-ttu-id="adca4-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="adca4-282">NUMC</span></span> | <span data-ttu-id="adca4-283">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-283">String</span></span>
<span data-ttu-id="adca4-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="adca4-284">TIMS</span></span> | <span data-ttu-id="adca4-285">Ciąg</span><span class="sxs-lookup"><span data-stu-id="adca4-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="adca4-286">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="adca4-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="adca4-287">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="adca4-287">Map source toosink columns</span></span>
<span data-ttu-id="adca4-288">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="adca4-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="adca4-289">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="adca4-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="adca4-290">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="adca4-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="adca4-291">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="adca4-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="adca4-292">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="adca4-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="adca4-293">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="adca4-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="adca4-294">Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="adca4-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="adca4-295">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="adca4-295">Performance and Tuning</span></span>
<span data-ttu-id="adca4-296">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="adca4-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
