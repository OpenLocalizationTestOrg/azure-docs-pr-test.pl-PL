---
title: "aaaMove danych SAP HANA przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych SAP HANA przy użyciu fabryki danych Azure."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="e5a4d-103">Przenoszenie danych z SAP HANA przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="e5a4d-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="e5a4d-104">W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z lokalnymi SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="e5a4d-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="e5a4d-106">Można skopiować danych z lokalnego SAP HANA magazynu tooany obsługiwane ujścia danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="e5a4d-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e5a4d-108">Fabryka danych aktualnie obsługuje tylko do przenoszenia danych z danych tooother SAP HANA przechowuje, ale nie w przypadku przenoszenia danych z innych danych przechowują tooan SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="e5a4d-109">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="e5a4d-109">Supported versions and installation</span></span>
<span data-ttu-id="e5a4d-110">Ten łącznik obsługuje dowolnej wersji bazy danych SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="e5a4d-111">Obsługuje ona kopiowanie danych z tabel wierszy i kolumn, za pomocą zapytań SQL i HANA modelach informacji (takich jak widoki analityczne i obliczeń).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="e5a4d-112">tooenable hello łączności toohello wystąpieniem SAP HANA zainstalować hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="e5a4d-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="e5a4d-113">**Brama zarządzania danymi**: połączenie lokalne tooon danych obsługuje usługi fabryka danych magazynów (w tym SAP HANA) przy użyciu składnika o nazwie brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="e5a4d-114">Zobacz toolearn o brama zarządzania danymi i szczegółowe instrukcje dotyczące konfigurowania bramy hello [przenoszenie danych między danymi lokalnymi przechowywany magazyn danych toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="e5a4d-115">Nawet jeśli hello SAP HANA znajduje się na maszynie wirtualnej platformy Azure IaaS (VM), wymagana jest brama.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="e5a4d-116">Możesz zainstalować bramę hello na powitania tej samej maszyny Wirtualnej jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="e5a4d-117">**Sterownik SAP HANA ODBC** na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="e5a4d-118">Sterownik SAP HANA ODBC hello można pobrać z hello [Centrum pobierania oprogramowania SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="e5a4d-119">Wyszukiwanie przy użyciu słowa kluczowego hello **SAP HANA klienta dla systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="e5a4d-120">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e5a4d-120">Getting started</span></span>
<span data-ttu-id="e5a4d-121">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="e5a4d-122">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e5a4d-123">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="e5a4d-124">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e5a4d-125">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e5a4d-126">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="e5a4d-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="e5a4d-127">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e5a4d-128">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="e5a4d-129">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e5a4d-130">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e5a4d-131">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e5a4d-132">Przykładowy z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z lokalnego SAP HANA [przykład JSON: kopiowanie danych z programu SAP HANA tooAzure obiektu Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e5a4d-133">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych SAP HANA tooan określonych jednostek fabryki danych używanych toodefine:</span><span class="sxs-lookup"><span data-stu-id="e5a4d-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e5a4d-134">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="e5a4d-134">Linked service properties</span></span>
<span data-ttu-id="e5a4d-135">Witaj w poniższej tabeli zawiera opis JSON elementy określonych tooSAP HANA połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="e5a4d-136">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e5a4d-136">Property</span></span> | <span data-ttu-id="e5a4d-137">Opis</span><span class="sxs-lookup"><span data-stu-id="e5a4d-137">Description</span></span> | <span data-ttu-id="e5a4d-138">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="e5a4d-138">Allowed values</span></span> | <span data-ttu-id="e5a4d-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e5a4d-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="e5a4d-140">serwer</span><span class="sxs-lookup"><span data-stu-id="e5a4d-140">server</span></span> | <span data-ttu-id="e5a4d-141">Nazwa serwera hello, na które hello SAP HANA znajduje się wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="e5a4d-142">Jeśli serwer używa portu dostosowane, określ `server:port`.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="e5a4d-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-143">string</span></span> | <span data-ttu-id="e5a4d-144">Tak</span><span class="sxs-lookup"><span data-stu-id="e5a4d-144">Yes</span></span>
<span data-ttu-id="e5a4d-145">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="e5a4d-145">authenticationType</span></span> | <span data-ttu-id="e5a4d-146">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-146">Type of authentication.</span></span> | <span data-ttu-id="e5a4d-147">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-147">string.</span></span> <span data-ttu-id="e5a4d-148">"Basic" lub "Windows"</span><span class="sxs-lookup"><span data-stu-id="e5a4d-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="e5a4d-149">Tak</span><span class="sxs-lookup"><span data-stu-id="e5a4d-149">Yes</span></span> 
<span data-ttu-id="e5a4d-150">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="e5a4d-150">username</span></span> | <span data-ttu-id="e5a4d-151">Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera</span><span class="sxs-lookup"><span data-stu-id="e5a4d-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="e5a4d-152">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-152">string</span></span> | <span data-ttu-id="e5a4d-153">Tak</span><span class="sxs-lookup"><span data-stu-id="e5a4d-153">Yes</span></span>
<span data-ttu-id="e5a4d-154">hasło</span><span class="sxs-lookup"><span data-stu-id="e5a4d-154">password</span></span> | <span data-ttu-id="e5a4d-155">Hasło dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-155">Password for hello user.</span></span> | <span data-ttu-id="e5a4d-156">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-156">string</span></span> | <span data-ttu-id="e5a4d-157">Tak</span><span class="sxs-lookup"><span data-stu-id="e5a4d-157">Yes</span></span>
<span data-ttu-id="e5a4d-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e5a4d-158">gatewayName</span></span> | <span data-ttu-id="e5a4d-159">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego SAP HANA wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="e5a4d-160">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-160">string</span></span> | <span data-ttu-id="e5a4d-161">Tak</span><span class="sxs-lookup"><span data-stu-id="e5a4d-161">Yes</span></span>
<span data-ttu-id="e5a4d-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e5a4d-162">encryptedCredential</span></span> | <span data-ttu-id="e5a4d-163">Witaj zaszyfrowanego ciągu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-163">hello encrypted credential string.</span></span> | <span data-ttu-id="e5a4d-164">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-164">string</span></span> | <span data-ttu-id="e5a4d-165">Nie</span><span class="sxs-lookup"><span data-stu-id="e5a4d-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="e5a4d-166">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="e5a4d-166">Dataset properties</span></span>
<span data-ttu-id="e5a4d-167">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e5a4d-168">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e5a4d-169">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e5a4d-170">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP HANA hello typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="e5a4d-171">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="e5a4d-171">Copy activity properties</span></span>
<span data-ttu-id="e5a4d-172">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e5a4d-173">Właściwości, takie jak nazwa, opis i tabel wejściowych i wyjściowych, czy zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="e5a4d-174">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="e5a4d-175">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="e5a4d-176">Gdy źródło w przypadku działania kopiowania jest typu **RelationalSource** (która obejmuje SAP HANA), hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="e5a4d-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="e5a4d-177">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e5a4d-177">Property</span></span> | <span data-ttu-id="e5a4d-178">Opis</span><span class="sxs-lookup"><span data-stu-id="e5a4d-178">Description</span></span> | <span data-ttu-id="e5a4d-179">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="e5a4d-179">Allowed values</span></span> | <span data-ttu-id="e5a4d-180">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e5a4d-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5a4d-181">query</span><span class="sxs-lookup"><span data-stu-id="e5a4d-181">query</span></span> | <span data-ttu-id="e5a4d-182">Określa hello SQL tooread dane z wystąpieniem SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="e5a4d-183">Zapytanie SQL.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-183">SQL query.</span></span> | <span data-ttu-id="e5a4d-184">Tak</span><span class="sxs-lookup"><span data-stu-id="e5a4d-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="e5a4d-185">Przykład JSON: kopiowanie danych z programu SAP HANA tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e5a4d-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="e5a4d-186">Witaj poniższy przykład zawiera definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e5a4d-187">W tym przykładzie pokazano sposób toocopy danych z lokalnego SAP HANA tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="e5a4d-188">Jednak dane mogą być kopiowane **bezpośrednio** tooany wychwytywanie hello wymienione [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e5a4d-189">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="e5a4d-190">Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="e5a4d-191">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="e5a4d-192">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="e5a4d-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="e5a4d-193">Połączonej usługi typu [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="e5a4d-194">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e5a4d-195">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="e5a4d-196">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e5a4d-197">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e5a4d-198">przykład Witaj co godzinę kopiuje dane z SAP HANA tooan wystąpienia obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="e5a4d-199">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e5a4d-200">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="e5a4d-201">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="e5a4d-202">SAP HANA połączone usługi</span><span class="sxs-lookup"><span data-stu-id="e5a4d-202">SAP HANA linked service</span></span>
<span data-ttu-id="e5a4d-203">To połączone usługi łączy fabrykę danych SAP HANA toohello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="e5a4d-204">Właściwość type Hello ustawiono zbyt**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="e5a4d-205">Hello typeProperties sekcja zawiera informacje o połączeniu dla hello wystąpienia SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="e5a4d-206">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e5a4d-206">Azure Storage linked service</span></span>
<span data-ttu-id="e5a4d-207">To połączone usługi łączy fabrykę danych toohello konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="e5a4d-208">Właściwość type Hello ustawiono zbyt**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="e5a4d-209">Witaj typeProperties sekcja zawiera informacje o połączeniu dla hello konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="e5a4d-210">Zestaw danych wejściowych SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e5a4d-210">SAP HANA input dataset</span></span>

<span data-ttu-id="e5a4d-211">Ten zestaw danych definiuje zestaw danych SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="e5a4d-212">Zbyt Ustaw typ hello DataSet fabryki danych hello**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="e5a4d-213">Obecnie nie określisz żadnych właściwości określonego typu dla zestawu danych SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="e5a4d-214">Zapytanie Hello w definicji działania kopiowania hello określa jakie tooread danych z hello wystąpienia SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="e5a4d-215">Ustawienie właściwości external tootrue informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="e5a4d-216">Częstotliwość i interwał właściwości definiuje hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="e5a4d-217">W takim przypadku hello dane są odczytywane z wystąpieniem SAP HANA hello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="e5a4d-218">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5a4d-218">Azure Blob output dataset</span></span>
<span data-ttu-id="e5a4d-219">Ten zestaw danych definiuje hello wyjściowego obiektu Blob systemu Azure zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="e5a4d-220">ustawiono tooAzureBlob Hello typu właściwości.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="e5a4d-221">sekcja typeProperties Hello zawiera, których są przechowywane dane hello skopiowane z hello SAP HANA wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="e5a4d-222">Hello są zapisywane dane nowego obiektu blob tooa co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e5a4d-223">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e5a4d-224">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="e5a4d-225">W potoku z działanie kopiowania</span><span class="sxs-lookup"><span data-stu-id="e5a4d-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="e5a4d-226">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e5a4d-227">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** (dla źródła SAP HANA) i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="e5a4d-228">Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="e5a4d-229">Mapowanie typu dla SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e5a4d-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="e5a4d-230">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:</span><span class="sxs-lookup"><span data-stu-id="e5a4d-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="e5a4d-231">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="e5a4d-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="e5a4d-232">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="e5a4d-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="e5a4d-233">Podczas przenoszenia danych z programu SAP HANA, następujące mapowania hello są używane z typów too.NET typy SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="e5a4d-234">SAP HANA typu</span><span class="sxs-lookup"><span data-stu-id="e5a4d-234">SAP HANA Type</span></span> | <span data-ttu-id="e5a4d-235">Typ na podstawie .NET</span><span class="sxs-lookup"><span data-stu-id="e5a4d-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="e5a4d-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="e5a4d-236">TINYINT</span></span> | <span data-ttu-id="e5a4d-237">Bajtów</span><span class="sxs-lookup"><span data-stu-id="e5a4d-237">Byte</span></span>
<span data-ttu-id="e5a4d-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="e5a4d-238">SMALLINT</span></span> | <span data-ttu-id="e5a4d-239">Int16</span><span class="sxs-lookup"><span data-stu-id="e5a4d-239">Int16</span></span>
<span data-ttu-id="e5a4d-240">INT</span><span class="sxs-lookup"><span data-stu-id="e5a4d-240">INT</span></span> | <span data-ttu-id="e5a4d-241">Int32</span><span class="sxs-lookup"><span data-stu-id="e5a4d-241">Int32</span></span>
<span data-ttu-id="e5a4d-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="e5a4d-242">BIGINT</span></span> | <span data-ttu-id="e5a4d-243">Int64</span><span class="sxs-lookup"><span data-stu-id="e5a4d-243">Int64</span></span>
<span data-ttu-id="e5a4d-244">RZECZYWISTE</span><span class="sxs-lookup"><span data-stu-id="e5a4d-244">REAL</span></span> | <span data-ttu-id="e5a4d-245">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="e5a4d-245">Single</span></span>
<span data-ttu-id="e5a4d-246">O PODWÓJNEJ PRECYZJI</span><span class="sxs-lookup"><span data-stu-id="e5a4d-246">DOUBLE</span></span> | <span data-ttu-id="e5a4d-247">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="e5a4d-247">Single</span></span>
<span data-ttu-id="e5a4d-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="e5a4d-248">DECIMAL</span></span> | <span data-ttu-id="e5a4d-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="e5a4d-249">Decimal</span></span>
<span data-ttu-id="e5a4d-250">WARTOŚĆ LOGICZNA</span><span class="sxs-lookup"><span data-stu-id="e5a4d-250">BOOLEAN</span></span> | <span data-ttu-id="e5a4d-251">Bajtów</span><span class="sxs-lookup"><span data-stu-id="e5a4d-251">Byte</span></span>
<span data-ttu-id="e5a4d-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="e5a4d-252">VARCHAR</span></span> | <span data-ttu-id="e5a4d-253">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-253">String</span></span>
<span data-ttu-id="e5a4d-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="e5a4d-254">NVARCHAR</span></span> | <span data-ttu-id="e5a4d-255">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-255">String</span></span>
<span data-ttu-id="e5a4d-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="e5a4d-256">CLOB</span></span> | <span data-ttu-id="e5a4d-257">Byte]</span><span class="sxs-lookup"><span data-stu-id="e5a4d-257">Byte[]</span></span>
<span data-ttu-id="e5a4d-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="e5a4d-258">ALPHANUM</span></span> | <span data-ttu-id="e5a4d-259">Ciąg</span><span class="sxs-lookup"><span data-stu-id="e5a4d-259">String</span></span>
<span data-ttu-id="e5a4d-260">OBIEKT BLOB</span><span class="sxs-lookup"><span data-stu-id="e5a4d-260">BLOB</span></span> | <span data-ttu-id="e5a4d-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="e5a4d-261">Byte[]</span></span>
<span data-ttu-id="e5a4d-262">DATA</span><span class="sxs-lookup"><span data-stu-id="e5a4d-262">DATE</span></span> | <span data-ttu-id="e5a4d-263">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e5a4d-263">DateTime</span></span>
<span data-ttu-id="e5a4d-264">CZAS</span><span class="sxs-lookup"><span data-stu-id="e5a4d-264">TIME</span></span> | <span data-ttu-id="e5a4d-265">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="e5a4d-265">TimeSpan</span></span>
<span data-ttu-id="e5a4d-266">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="e5a4d-266">TIMESTAMP</span></span> | <span data-ttu-id="e5a4d-267">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e5a4d-267">DateTime</span></span>
<span data-ttu-id="e5a4d-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="e5a4d-268">SECONDDATE</span></span> | <span data-ttu-id="e5a4d-269">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e5a4d-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="e5a4d-270">Znane ograniczenia</span><span class="sxs-lookup"><span data-stu-id="e5a4d-270">Known limitations</span></span>
<span data-ttu-id="e5a4d-271">Podczas kopiowania danych z programu SAP HANA istnieje kilka znane ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="e5a4d-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="e5a4d-272">Ciągi NVARCHAR to toomaximum skróconą długość 4000 znaków Unicode</span><span class="sxs-lookup"><span data-stu-id="e5a4d-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="e5a4d-273">SMALLDECIMAL nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="e5a4d-274">VARBINARY nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="e5a4d-275">Prawidłowe daty należą do zakresu od 30-1899/12, a 9999-12/31</span><span class="sxs-lookup"><span data-stu-id="e5a4d-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="e5a4d-276">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="e5a4d-276">Map source toosink columns</span></span>
<span data-ttu-id="e5a4d-277">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e5a4d-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e5a4d-278">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="e5a4d-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="e5a4d-279">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="e5a4d-280">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e5a4d-281">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e5a4d-282">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e5a4d-283">Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="e5a4d-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e5a4d-284">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="e5a4d-284">Performance and Tuning</span></span>
<span data-ttu-id="e5a4d-285">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="e5a4d-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
