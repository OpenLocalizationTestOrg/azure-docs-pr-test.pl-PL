---
title: "Przenoszenie danych ze źródła OData | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z źródła OData przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="83fc4-103">Przenoszenie danych źródła z OData przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="83fc4-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="83fc4-104">W tym artykule opisano sposób korzystania działanie kopiowania w fabryce danych Azure, aby przenieść dane ze źródła danych OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="83fc4-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="83fc4-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="83fc4-106">Wszystkie obsługiwanych ujścia magazynu danych można skopiować danych ze źródła danych OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="83fc4-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="83fc4-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="83fc4-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, ze źródła danych OData do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych do źródła danych OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="83fc4-109">Obsługiwane wersje i typy uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="83fc4-109">Supported versions and authentication types</span></span>
<span data-ttu-id="83fc4-110">Ten łącznik OData obsługuje OData w wersji 3.0 i 4.0, a można skopiować danych z obu chmury OData i lokalnego źródła OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="83fc4-111">W przypadku drugiego nagłówka musisz zainstalować bramę zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="83fc4-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="83fc4-112">Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="83fc4-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="83fc4-113">Poniżej uwierzytelniania są obsługiwane typy:</span><span class="sxs-lookup"><span data-stu-id="83fc4-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="83fc4-114">Aby uzyskać dostęp do **chmury** źródła danych OData, można użyć anonimowe, podstawowe (nazwa użytkownika i hasło) lub Azure Active Directory na podstawie uwierzytelniania OAuth.</span><span class="sxs-lookup"><span data-stu-id="83fc4-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="83fc4-115">Aby uzyskać dostęp do **lokalnymi** źródła danych OData, możesz użyć anonimowe, basic (nazwa użytkownika i hasło) lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="83fc4-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="83fc4-116">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="83fc4-116">Getting started</span></span>
<span data-ttu-id="83fc4-117">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła danych OData przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="83fc4-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="83fc4-118">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="83fc4-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="83fc4-119">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="83fc4-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="83fc4-120">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="83fc4-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="83fc4-121">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="83fc4-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="83fc4-122">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="83fc4-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="83fc4-123">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="83fc4-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="83fc4-124">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="83fc4-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="83fc4-125">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="83fc4-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="83fc4-126">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="83fc4-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="83fc4-127">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="83fc4-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="83fc4-128">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do skopiowania danych ze źródła danych OData, zobacz [przykład JSON: kopiowanie danych z źródła OData do obiektów Blob platformy Azure](#json-example-copy-data-from-odata-source-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="83fc4-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="83fc4-129">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do źródła OData:</span><span class="sxs-lookup"><span data-stu-id="83fc4-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="83fc4-130">Właściwości usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="83fc4-130">Linked Service properties</span></span>
<span data-ttu-id="83fc4-131">Poniższa tabela zawiera opis specyficzne dla usługi OData połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="83fc4-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="83fc4-132">Właściwość</span><span class="sxs-lookup"><span data-stu-id="83fc4-132">Property</span></span> | <span data-ttu-id="83fc4-133">Opis</span><span class="sxs-lookup"><span data-stu-id="83fc4-133">Description</span></span> | <span data-ttu-id="83fc4-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="83fc4-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83fc4-135">type</span><span class="sxs-lookup"><span data-stu-id="83fc4-135">type</span></span> |<span data-ttu-id="83fc4-136">Właściwość type musi mieć ustawioną: **OData**</span><span class="sxs-lookup"><span data-stu-id="83fc4-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="83fc4-137">Tak</span><span class="sxs-lookup"><span data-stu-id="83fc4-137">Yes</span></span> |
| <span data-ttu-id="83fc4-138">adres URL</span><span class="sxs-lookup"><span data-stu-id="83fc4-138">url</span></span> |<span data-ttu-id="83fc4-139">Adres URL usługi OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-139">Url of the OData service.</span></span> |<span data-ttu-id="83fc4-140">Tak</span><span class="sxs-lookup"><span data-stu-id="83fc4-140">Yes</span></span> |
| <span data-ttu-id="83fc4-141">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="83fc4-141">authenticationType</span></span> |<span data-ttu-id="83fc4-142">Typ uwierzytelniania używany do nawiązania połączenia źródła OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="83fc4-143">Chmury OData możliwe wartości to anonimowe, podstawowe i OAuth (Uwaga obecnie tylko pomocy technicznej usługi fabryka danych Azure OAuth opartej na usłudze Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="83fc4-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="83fc4-144">Dla protokołu OData lokalnymi możliwe wartości to anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="83fc4-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="83fc4-145">Tak</span><span class="sxs-lookup"><span data-stu-id="83fc4-145">Yes</span></span> |
| <span data-ttu-id="83fc4-146">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="83fc4-146">username</span></span> |<span data-ttu-id="83fc4-147">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="83fc4-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="83fc4-148">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="83fc4-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="83fc4-149">hasło</span><span class="sxs-lookup"><span data-stu-id="83fc4-149">password</span></span> |<span data-ttu-id="83fc4-150">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="83fc4-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="83fc4-151">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="83fc4-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="83fc4-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="83fc4-152">authorizedCredential</span></span> |<span data-ttu-id="83fc4-153">Jeśli używasz uwierzytelniania OAuth, kliknij przycisk **autoryzacji** przycisku w kreatorze kopiowania fabryki danych lub edytorze, a następnie wprowadź Twoje poświadczenia wartość tej właściwości będzie wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="83fc4-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="83fc4-154">Tak (tylko wtedy, gdy używasz uwierzytelniania OAuth)</span><span class="sxs-lookup"><span data-stu-id="83fc4-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="83fc4-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="83fc4-155">gatewayName</span></span> |<span data-ttu-id="83fc4-156">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną usługą OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="83fc4-157">Określ tylko, jeśli dane są kopiowane z lokalnego źródła OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="83fc4-158">Nie</span><span class="sxs-lookup"><span data-stu-id="83fc4-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="83fc4-159">Przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="83fc4-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="83fc4-160">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="83fc4-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="83fc4-161">Przy użyciu uwierzytelniania systemu Windows podczas uzyskiwania dostępu do lokalnego źródła OData</span><span class="sxs-lookup"><span data-stu-id="83fc4-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="83fc4-162">Przy użyciu OAuth uwierzytelniania podczas uzyskiwania dostępu do chmury źródło OData</span><span class="sxs-lookup"><span data-stu-id="83fc4-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="83fc4-163">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="83fc4-163">Dataset properties</span></span>
<span data-ttu-id="83fc4-164">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="83fc4-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="83fc4-165">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="83fc4-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="83fc4-166">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="83fc4-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="83fc4-167">TypeProperties sekcja dla zestawu danych typu **ODataResource** (w tym zestawie danych OData) ma następujące właściwości</span><span class="sxs-lookup"><span data-stu-id="83fc4-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="83fc4-168">Właściwość</span><span class="sxs-lookup"><span data-stu-id="83fc4-168">Property</span></span> | <span data-ttu-id="83fc4-169">Opis</span><span class="sxs-lookup"><span data-stu-id="83fc4-169">Description</span></span> | <span data-ttu-id="83fc4-170">Wymagane</span><span class="sxs-lookup"><span data-stu-id="83fc4-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83fc4-171">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="83fc4-171">path</span></span> |<span data-ttu-id="83fc4-172">Ścieżka do zasobu OData</span><span class="sxs-lookup"><span data-stu-id="83fc4-172">Path to the OData resource</span></span> |<span data-ttu-id="83fc4-173">Nie</span><span class="sxs-lookup"><span data-stu-id="83fc4-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="83fc4-174">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="83fc4-174">Copy activity properties</span></span>
<span data-ttu-id="83fc4-175">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="83fc4-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="83fc4-176">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="83fc4-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="83fc4-177">Właściwości, które są dostępne w sekcji typeProperties działania z drugiej strony zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="83fc4-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="83fc4-178">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="83fc4-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="83fc4-179">Jeśli źródło jest typu **RelationalSource** (w tym OData) w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="83fc4-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="83fc4-180">Właściwość</span><span class="sxs-lookup"><span data-stu-id="83fc4-180">Property</span></span> | <span data-ttu-id="83fc4-181">Opis</span><span class="sxs-lookup"><span data-stu-id="83fc4-181">Description</span></span> | <span data-ttu-id="83fc4-182">Przykład</span><span class="sxs-lookup"><span data-stu-id="83fc4-182">Example</span></span> | <span data-ttu-id="83fc4-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="83fc4-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="83fc4-184">query</span><span class="sxs-lookup"><span data-stu-id="83fc4-184">query</span></span> |<span data-ttu-id="83fc4-185">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="83fc4-185">Use the custom query to read data.</span></span> |<span data-ttu-id="83fc4-186">"? $select = nazwa, opis i $top = 5"</span><span class="sxs-lookup"><span data-stu-id="83fc4-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="83fc4-187">Nie</span><span class="sxs-lookup"><span data-stu-id="83fc4-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="83fc4-188">Mapowanie typu dla protokołu OData</span><span class="sxs-lookup"><span data-stu-id="83fc4-188">Type Mapping for OData</span></span>
<span data-ttu-id="83fc4-189">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, automatyczne konwersje z typów źródła do zbiornika typy z następujących rozwinięcie wykonuje działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="83fc4-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="83fc4-190">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="83fc4-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="83fc4-191">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="83fc4-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="83fc4-192">Podczas przenoszenia danych z OData, następujące mapowania są używane typy OData do typ architektury .NET.</span><span class="sxs-lookup"><span data-stu-id="83fc4-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="83fc4-193">Typ danych OData</span><span class="sxs-lookup"><span data-stu-id="83fc4-193">OData Data Type</span></span> | <span data-ttu-id="83fc4-194">Typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="83fc4-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="83fc4-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="83fc4-195">Edm.Binary</span></span> |<span data-ttu-id="83fc4-196">Byte]</span><span class="sxs-lookup"><span data-stu-id="83fc4-196">Byte[]</span></span> |
| <span data-ttu-id="83fc4-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="83fc4-197">Edm.Boolean</span></span> |<span data-ttu-id="83fc4-198">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="83fc4-198">Bool</span></span> |
| <span data-ttu-id="83fc4-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="83fc4-199">Edm.Byte</span></span> |<span data-ttu-id="83fc4-200">Byte]</span><span class="sxs-lookup"><span data-stu-id="83fc4-200">Byte[]</span></span> |
| <span data-ttu-id="83fc4-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="83fc4-201">Edm.DateTime</span></span> |<span data-ttu-id="83fc4-202">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="83fc4-202">DateTime</span></span> |
| <span data-ttu-id="83fc4-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="83fc4-203">Edm.Decimal</span></span> |<span data-ttu-id="83fc4-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="83fc4-204">Decimal</span></span> |
| <span data-ttu-id="83fc4-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="83fc4-205">Edm.Double</span></span> |<span data-ttu-id="83fc4-206">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="83fc4-206">Double</span></span> |
| <span data-ttu-id="83fc4-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="83fc4-207">Edm.Single</span></span> |<span data-ttu-id="83fc4-208">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="83fc4-208">Single</span></span> |
| <span data-ttu-id="83fc4-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="83fc4-209">Edm.Guid</span></span> |<span data-ttu-id="83fc4-210">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="83fc4-210">Guid</span></span> |
| <span data-ttu-id="83fc4-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="83fc4-211">Edm.Int16</span></span> |<span data-ttu-id="83fc4-212">Int16</span><span class="sxs-lookup"><span data-stu-id="83fc4-212">Int16</span></span> |
| <span data-ttu-id="83fc4-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="83fc4-213">Edm.Int32</span></span> |<span data-ttu-id="83fc4-214">Int32</span><span class="sxs-lookup"><span data-stu-id="83fc4-214">Int32</span></span> |
| <span data-ttu-id="83fc4-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="83fc4-215">Edm.Int64</span></span> |<span data-ttu-id="83fc4-216">Int64</span><span class="sxs-lookup"><span data-stu-id="83fc4-216">Int64</span></span> |
| <span data-ttu-id="83fc4-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="83fc4-217">Edm.SByte</span></span> |<span data-ttu-id="83fc4-218">Int16</span><span class="sxs-lookup"><span data-stu-id="83fc4-218">Int16</span></span> |
| <span data-ttu-id="83fc4-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="83fc4-219">Edm.String</span></span> |<span data-ttu-id="83fc4-220">Ciąg</span><span class="sxs-lookup"><span data-stu-id="83fc4-220">String</span></span> |
| <span data-ttu-id="83fc4-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="83fc4-221">Edm.Time</span></span> |<span data-ttu-id="83fc4-222">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="83fc4-222">TimeSpan</span></span> |
| <span data-ttu-id="83fc4-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="83fc4-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="83fc4-224">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="83fc4-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="83fc4-225">Typy złożone danych OData np. obiektu nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="83fc4-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="83fc4-226">Przykład JSON: kopiowanie danych z źródła OData do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="83fc4-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="83fc4-227">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="83fc4-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="83fc4-228">Przedstawiają sposób kopiowania danych ze źródła danych OData do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="83fc4-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="83fc4-229">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="83fc4-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="83fc4-230">Przykład zawiera następujące jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="83fc4-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="83fc4-231">Połączonej usługi typu [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="83fc4-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="83fc4-232">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="83fc4-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="83fc4-233">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="83fc4-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="83fc4-234">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="83fc4-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="83fc4-235">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="83fc4-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="83fc4-236">Przykład kopiuje dane z zapytań względem źródła OData do obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="83fc4-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="83fc4-237">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="83fc4-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="83fc4-238">**OData połączonej usługi:** w tym przykładzie użyto uwierzytelnianie anonimowe.</span><span class="sxs-lookup"><span data-stu-id="83fc4-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="83fc4-239">Zobacz [OData połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="83fc4-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="83fc4-240">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="83fc4-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="83fc4-241">**Wejściowy zestaw danych OData:**</span><span class="sxs-lookup"><span data-stu-id="83fc4-241">**OData input dataset:**</span></span>

<span data-ttu-id="83fc4-242">Ustawienie "external": "prawda" informuje usługi fabryka danych czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="83fc4-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="83fc4-243">Określanie **ścieżki** w zestawie danych definicji jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="83fc4-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="83fc4-244">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="83fc4-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="83fc4-245">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="83fc4-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="83fc4-246">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="83fc4-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="83fc4-247">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="83fc4-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="83fc4-248">**Aktywność kopiowania w potoku z OData źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="83fc4-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="83fc4-249">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="83fc4-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="83fc4-250">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="83fc4-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="83fc4-251">Określony dla zapytania SQL **zapytania** właściwości wybiera (Najnowsza) najnowsze dane ze źródła OData.</span><span class="sxs-lookup"><span data-stu-id="83fc4-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

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

<span data-ttu-id="83fc4-252">Określanie **zapytania** w potoku definicji jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="83fc4-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="83fc4-253">**Adres URL** jest używany do pobierania danych usługi fabryka danych z: adres URL określony w połączonej usłudze (wymagane) + ścieżka zestawu danych (opcjonalnie) + zapytania w potoku (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="83fc4-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="83fc4-254">Mapowanie typu dla protokołu OData</span><span class="sxs-lookup"><span data-stu-id="83fc4-254">Type mapping for OData</span></span>
<span data-ttu-id="83fc4-255">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, wykonuje działanie kopiowania automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="83fc4-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="83fc4-256">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="83fc4-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="83fc4-257">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="83fc4-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="83fc4-258">Jeśli przechowuje przenoszenie danych ze źródła danych OData, typy danych OData są mapowane do typów .NET.</span><span class="sxs-lookup"><span data-stu-id="83fc4-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="83fc4-259">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="83fc4-259">Map source to sink columns</span></span>
<span data-ttu-id="83fc4-260">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="83fc4-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="83fc4-261">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="83fc4-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="83fc4-262">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="83fc4-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="83fc4-263">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="83fc4-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="83fc4-264">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="83fc4-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="83fc4-265">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="83fc4-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="83fc4-266">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="83fc4-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="83fc4-267">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="83fc4-267">Performance and Tuning</span></span>
<span data-ttu-id="83fc4-268">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="83fc4-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
