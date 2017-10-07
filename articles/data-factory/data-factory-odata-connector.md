---
title: "aaaMove danych ze źródeł OData | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove z OData źródła przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="4e671-103">Przenoszenie danych źródła z OData przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="4e671-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="4e671-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych ze źródła danych OData.</span><span class="sxs-lookup"><span data-stu-id="4e671-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="4e671-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4e671-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="4e671-106">Można skopiować danych z magazynu danych zbiornika tooany obsługiwane źródła OData.</span><span class="sxs-lookup"><span data-stu-id="4e671-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="4e671-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="4e671-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4e671-108">Fabryka danych aktualnie obsługuje tylko do przenoszenia danych z danych tooother źródła OData przechowuje, ale nie w przypadku przenoszenia danych z innych danych przechowują tooan źródło OData.</span><span class="sxs-lookup"><span data-stu-id="4e671-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="4e671-109">Obsługiwane wersje i typy uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="4e671-109">Supported versions and authentication types</span></span>
<span data-ttu-id="4e671-110">Ten łącznik OData obsługuje OData w wersji 3.0 i 4.0, a można skopiować danych z obu chmury OData i lokalnego źródła OData.</span><span class="sxs-lookup"><span data-stu-id="4e671-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="4e671-111">Hello później należy hello tooinstall brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="4e671-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="4e671-112">Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="4e671-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="4e671-113">Poniżej uwierzytelniania są obsługiwane typy:</span><span class="sxs-lookup"><span data-stu-id="4e671-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="4e671-114">tooaccess **chmury** źródła danych OData, można użyć anonimowe, podstawowe (nazwa użytkownika i hasło) lub Azure Active Directory na podstawie uwierzytelniania OAuth.</span><span class="sxs-lookup"><span data-stu-id="4e671-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="4e671-115">tooaccess **lokalnymi** źródła danych OData, możesz użyć anonimowe, podstawowe (nazwa użytkownika i hasło) lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4e671-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4e671-116">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="4e671-116">Getting started</span></span>
<span data-ttu-id="4e671-117">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła danych OData przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="4e671-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="4e671-118">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="4e671-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4e671-119">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="4e671-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="4e671-120">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="4e671-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4e671-121">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4e671-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4e671-122">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="4e671-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="4e671-123">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4e671-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4e671-124">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4e671-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="4e671-125">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4e671-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4e671-126">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="4e671-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4e671-127">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4e671-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4e671-128">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych ze źródła danych OData, zobacz [przykład JSON: kopiowanie danych z tooAzure źródła OData Blob](#json-example-copy-data-from-odata-source-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="4e671-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="4e671-129">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek tooOData określonego źródła:</span><span class="sxs-lookup"><span data-stu-id="4e671-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4e671-130">Właściwości usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="4e671-130">Linked Service properties</span></span>
<span data-ttu-id="4e671-131">Hello w poniższej tabeli przedstawiono opis usługi określonego tooOData połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="4e671-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="4e671-132">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e671-132">Property</span></span> | <span data-ttu-id="4e671-133">Opis</span><span class="sxs-lookup"><span data-stu-id="4e671-133">Description</span></span> | <span data-ttu-id="4e671-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4e671-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e671-135">type</span><span class="sxs-lookup"><span data-stu-id="4e671-135">type</span></span> |<span data-ttu-id="4e671-136">musi mieć ustawioną właściwość type Hello: **OData**</span><span class="sxs-lookup"><span data-stu-id="4e671-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="4e671-137">Tak</span><span class="sxs-lookup"><span data-stu-id="4e671-137">Yes</span></span> |
| <span data-ttu-id="4e671-138">adres URL</span><span class="sxs-lookup"><span data-stu-id="4e671-138">url</span></span> |<span data-ttu-id="4e671-139">Adres URL usługi OData hello.</span><span class="sxs-lookup"><span data-stu-id="4e671-139">Url of hello OData service.</span></span> |<span data-ttu-id="4e671-140">Tak</span><span class="sxs-lookup"><span data-stu-id="4e671-140">Yes</span></span> |
| <span data-ttu-id="4e671-141">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="4e671-141">authenticationType</span></span> |<span data-ttu-id="4e671-142">Typ uwierzytelniania używany źródło OData toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4e671-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="4e671-143">Chmury OData możliwe wartości to anonimowe, podstawowe i OAuth (Uwaga obecnie tylko pomocy technicznej usługi fabryka danych Azure OAuth opartej na usłudze Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4e671-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="4e671-144">Dla protokołu OData lokalnymi możliwe wartości to anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4e671-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="4e671-145">Tak</span><span class="sxs-lookup"><span data-stu-id="4e671-145">Yes</span></span> |
| <span data-ttu-id="4e671-146">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="4e671-146">username</span></span> |<span data-ttu-id="4e671-147">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="4e671-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="4e671-148">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="4e671-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="4e671-149">hasło</span><span class="sxs-lookup"><span data-stu-id="4e671-149">password</span></span> |<span data-ttu-id="4e671-150">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4e671-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="4e671-151">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="4e671-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="4e671-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="4e671-152">authorizedCredential</span></span> |<span data-ttu-id="4e671-153">Jeśli używasz uwierzytelniania OAuth, kliknij przycisk **autoryzacji** przycisku na powitania Kreatora kopiowania fabryki danych lub edytorze, a następnie wprowadź Twoje poświadczenia hello wartość tej właściwości będzie wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="4e671-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="4e671-154">Tak (tylko wtedy, gdy używasz uwierzytelniania OAuth)</span><span class="sxs-lookup"><span data-stu-id="4e671-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="4e671-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4e671-155">gatewayName</span></span> |<span data-ttu-id="4e671-156">Nazwa bramy hello hello usługi fabryka danych należy używać usługi OData lokalnymi toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4e671-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="4e671-157">Określ tylko, jeśli dane są kopiowane z lokalnego źródła OData.</span><span class="sxs-lookup"><span data-stu-id="4e671-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="4e671-158">Nie</span><span class="sxs-lookup"><span data-stu-id="4e671-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="4e671-159">Przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="4e671-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="4e671-160">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="4e671-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="4e671-161">Przy użyciu uwierzytelniania systemu Windows podczas uzyskiwania dostępu do lokalnego źródła OData</span><span class="sxs-lookup"><span data-stu-id="4e671-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="4e671-162">Przy użyciu OAuth uwierzytelniania podczas uzyskiwania dostępu do chmury źródło OData</span><span class="sxs-lookup"><span data-stu-id="4e671-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="4e671-163">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="4e671-163">Dataset properties</span></span>
<span data-ttu-id="4e671-164">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="4e671-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4e671-165">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="4e671-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="4e671-166">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="4e671-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="4e671-167">Witaj typeProperties sekcja dla zestawu danych typu **ODataResource** (w tym zestawie danych OData) ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="4e671-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="4e671-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e671-168">Property</span></span> | <span data-ttu-id="4e671-169">Opis</span><span class="sxs-lookup"><span data-stu-id="4e671-169">Description</span></span> | <span data-ttu-id="4e671-170">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4e671-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e671-171">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="4e671-171">path</span></span> |<span data-ttu-id="4e671-172">Toohello ścieżki OData zasobów</span><span class="sxs-lookup"><span data-stu-id="4e671-172">Path toohello OData resource</span></span> |<span data-ttu-id="4e671-173">Nie</span><span class="sxs-lookup"><span data-stu-id="4e671-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="4e671-174">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="4e671-174">Copy activity properties</span></span>
<span data-ttu-id="4e671-175">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="4e671-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4e671-176">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="4e671-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="4e671-177">Właściwości dostępne w sekcji typeProperties hello aktywności hello na powitania drugiej zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="4e671-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="4e671-178">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="4e671-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4e671-179">Jeśli źródło jest typu **RelationalSource** (w tym OData) hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="4e671-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="4e671-180">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e671-180">Property</span></span> | <span data-ttu-id="4e671-181">Opis</span><span class="sxs-lookup"><span data-stu-id="4e671-181">Description</span></span> | <span data-ttu-id="4e671-182">Przykład</span><span class="sxs-lookup"><span data-stu-id="4e671-182">Example</span></span> | <span data-ttu-id="4e671-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4e671-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4e671-184">query</span><span class="sxs-lookup"><span data-stu-id="4e671-184">query</span></span> |<span data-ttu-id="4e671-185">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="4e671-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="4e671-186">"? $select = nazwa, opis i $top = 5"</span><span class="sxs-lookup"><span data-stu-id="4e671-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="4e671-187">Nie</span><span class="sxs-lookup"><span data-stu-id="4e671-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="4e671-188">Mapowanie typu dla protokołu OData</span><span class="sxs-lookup"><span data-stu-id="4e671-188">Type Mapping for OData</span></span>
<span data-ttu-id="4e671-189">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie.</span><span class="sxs-lookup"><span data-stu-id="4e671-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="4e671-190">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="4e671-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="4e671-191">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="4e671-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="4e671-192">Podczas przenoszenia danych z OData, hello następujące mapowania są używane z typu too.NET typy OData.</span><span class="sxs-lookup"><span data-stu-id="4e671-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="4e671-193">Typ danych OData</span><span class="sxs-lookup"><span data-stu-id="4e671-193">OData Data Type</span></span> | <span data-ttu-id="4e671-194">Typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="4e671-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="4e671-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="4e671-195">Edm.Binary</span></span> |<span data-ttu-id="4e671-196">Byte]</span><span class="sxs-lookup"><span data-stu-id="4e671-196">Byte[]</span></span> |
| <span data-ttu-id="4e671-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="4e671-197">Edm.Boolean</span></span> |<span data-ttu-id="4e671-198">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="4e671-198">Bool</span></span> |
| <span data-ttu-id="4e671-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="4e671-199">Edm.Byte</span></span> |<span data-ttu-id="4e671-200">Byte]</span><span class="sxs-lookup"><span data-stu-id="4e671-200">Byte[]</span></span> |
| <span data-ttu-id="4e671-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="4e671-201">Edm.DateTime</span></span> |<span data-ttu-id="4e671-202">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="4e671-202">DateTime</span></span> |
| <span data-ttu-id="4e671-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="4e671-203">Edm.Decimal</span></span> |<span data-ttu-id="4e671-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="4e671-204">Decimal</span></span> |
| <span data-ttu-id="4e671-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="4e671-205">Edm.Double</span></span> |<span data-ttu-id="4e671-206">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="4e671-206">Double</span></span> |
| <span data-ttu-id="4e671-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="4e671-207">Edm.Single</span></span> |<span data-ttu-id="4e671-208">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="4e671-208">Single</span></span> |
| <span data-ttu-id="4e671-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="4e671-209">Edm.Guid</span></span> |<span data-ttu-id="4e671-210">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="4e671-210">Guid</span></span> |
| <span data-ttu-id="4e671-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="4e671-211">Edm.Int16</span></span> |<span data-ttu-id="4e671-212">Int16</span><span class="sxs-lookup"><span data-stu-id="4e671-212">Int16</span></span> |
| <span data-ttu-id="4e671-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="4e671-213">Edm.Int32</span></span> |<span data-ttu-id="4e671-214">Int32</span><span class="sxs-lookup"><span data-stu-id="4e671-214">Int32</span></span> |
| <span data-ttu-id="4e671-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="4e671-215">Edm.Int64</span></span> |<span data-ttu-id="4e671-216">Int64</span><span class="sxs-lookup"><span data-stu-id="4e671-216">Int64</span></span> |
| <span data-ttu-id="4e671-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="4e671-217">Edm.SByte</span></span> |<span data-ttu-id="4e671-218">Int16</span><span class="sxs-lookup"><span data-stu-id="4e671-218">Int16</span></span> |
| <span data-ttu-id="4e671-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="4e671-219">Edm.String</span></span> |<span data-ttu-id="4e671-220">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4e671-220">String</span></span> |
| <span data-ttu-id="4e671-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="4e671-221">Edm.Time</span></span> |<span data-ttu-id="4e671-222">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="4e671-222">TimeSpan</span></span> |
| <span data-ttu-id="4e671-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="4e671-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="4e671-224">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="4e671-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="4e671-225">Typy złożone danych OData np. obiektu nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4e671-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="4e671-226">Przykład JSON: kopiowanie danych z tooAzure źródła OData obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="4e671-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="4e671-227">W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4e671-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4e671-228">Przedstawiają sposób toocopy danych OData źródła tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4e671-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="4e671-229">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="4e671-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="4e671-230">przykład Witaj ma powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="4e671-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="4e671-231">Połączonej usługi typu [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4e671-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="4e671-232">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4e671-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4e671-233">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4e671-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="4e671-234">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4e671-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4e671-235">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4e671-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4e671-236">przykład Witaj kopiuje dane z zapytaniach dotyczących tooan źródła OData obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="4e671-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="4e671-237">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="4e671-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="4e671-238">**OData połączonej usługi:** w tym przykładzie używa hello uwierzytelnianie anonimowe.</span><span class="sxs-lookup"><span data-stu-id="4e671-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="4e671-239">Zobacz [OData połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="4e671-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="4e671-240">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="4e671-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="4e671-241">**Wejściowy zestaw danych OData:**</span><span class="sxs-lookup"><span data-stu-id="4e671-241">**OData input dataset:**</span></span>

<span data-ttu-id="4e671-242">Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="4e671-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="4e671-243">Określanie **ścieżki** w zestawie danych hello definicji jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="4e671-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="4e671-244">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="4e671-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="4e671-245">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="4e671-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4e671-246">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="4e671-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4e671-247">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="4e671-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="4e671-248">**Aktywność kopiowania w potoku z OData źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="4e671-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="4e671-249">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="4e671-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="4e671-250">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4e671-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="4e671-251">Zapytanie SQL Hello określone dla hello **zapytania** właściwości wybiera hello najnowsze dane (Najnowsza) z hello źródło OData.</span><span class="sxs-lookup"><span data-stu-id="4e671-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="4e671-252">Określanie **zapytania** w potoku hello definicji jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="4e671-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="4e671-253">Hello **adres URL** jest używany usługi fabryka danych hello danych tooretrieve: adres URL określony w hello połączonej usługi (wymagane) + ścieżki określonej w elemencie dataset hello (opcjonalnie) + zapytania w potoku hello (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="4e671-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="4e671-254">Mapowanie typu dla protokołu OData</span><span class="sxs-lookup"><span data-stu-id="4e671-254">Type mapping for OData</span></span>
<span data-ttu-id="4e671-255">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="4e671-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="4e671-256">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="4e671-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="4e671-257">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="4e671-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="4e671-258">Podczas przenoszenia danych z baz danych OData, typy danych OData są mapowane too.NET typów.</span><span class="sxs-lookup"><span data-stu-id="4e671-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="4e671-259">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="4e671-259">Map source toosink columns</span></span>
<span data-ttu-id="4e671-260">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4e671-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4e671-261">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="4e671-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="4e671-262">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="4e671-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="4e671-263">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="4e671-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4e671-264">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="4e671-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4e671-265">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="4e671-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="4e671-266">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="4e671-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4e671-267">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="4e671-267">Performance and Tuning</span></span>
<span data-ttu-id="4e671-268">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="4e671-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
