---
title: "Przenieść dane z witryny Salesforce przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z usług Salesforce przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="c8927-103">Przenieść dane z witryny Salesforce przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="c8927-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="c8927-104">W tym artykule opisano, jak używasz działanie kopiowania w fabryce danych Azure można skopiować danych z usług Salesforce na dowolnym magazynem danych, który znajduje się w kolumnie zbiornika w [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="c8927-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c8927-105">W tym artykule opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z kombinacji magazynu obsługiwane dane i działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c8927-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="c8927-106">Fabryka danych Azure aktualnie obsługuje tylko przenoszenia danych z usługi Salesforce, aby [obsługiwane magazyny danych zbiornika](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ale nie obsługuje przenoszenia danych z innych danych przechowuje do usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c8927-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="c8927-107">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="c8927-107">Supported versions</span></span>
<span data-ttu-id="c8927-108">Ten łącznik obsługuje następujące wersje usług Salesforce: Developer Edition w wersji Professional, Enterprise Edition albo nieograniczone Edition.</span><span class="sxs-lookup"><span data-stu-id="c8927-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="c8927-109">I obsługuje kopiowanie z Salesforce produkcji, piaskownicy i domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="c8927-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8927-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c8927-110">Prerequisites</span></span>
* <span data-ttu-id="c8927-111">Musi być włączone uprawnienia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c8927-111">API permission must be enabled.</span></span> <span data-ttu-id="c8927-112">Zobacz [jak włączyć dostęp do interfejsu API w usłudze Salesforce przez zestaw uprawnień?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="c8927-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="c8927-113">Aby skopiować dane z witryny Salesforce do lokalnych magazynów danych, użytkownik musi mieć co najmniej 2.0 bramy zarządzania danych zainstalowanej w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="c8927-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="c8927-114">Limity żądań usług SalesForce</span><span class="sxs-lookup"><span data-stu-id="c8927-114">Salesforce request limits</span></span>
<span data-ttu-id="c8927-115">Usługa SalesForce obejmuje limity dla całkowita liczba żądań interfejsu API i równoczesnych żądań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c8927-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="c8927-116">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="c8927-116">Note the following points:</span></span>

- <span data-ttu-id="c8927-117">Jeśli liczba jednoczesnych żądań przekracza limit, ograniczanie występuje i będzie wyświetlany losowe awarie.</span><span class="sxs-lookup"><span data-stu-id="c8927-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="c8927-118">Jeśli całkowita liczba żądań przekracza limit, konta usług Salesforce jest blokowana przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="c8927-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="c8927-119">W obu przypadkach może być również wyświetlony błąd "REQUEST_LIMIT_EXCEEDED".</span><span class="sxs-lookup"><span data-stu-id="c8927-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="c8927-120">Zobacz sekcję "Limity żądań interfejsu API" w [Salesforce Developer limity](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c8927-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c8927-121">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c8927-121">Getting started</span></span>
<span data-ttu-id="c8927-122">Można utworzyć potok z działania kopiowania, który przenosi dane z witryny Salesforce przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="c8927-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="c8927-123">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="c8927-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c8927-124">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="c8927-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="c8927-125">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="c8927-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c8927-126">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c8927-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c8927-127">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="c8927-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="c8927-128">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="c8927-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c8927-129">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c8927-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c8927-130">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c8927-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c8927-131">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="c8927-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c8927-132">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="c8927-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c8927-133">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do skopiowania danych z usług Salesforce, zobacz [przykład JSON: kopiowanie danych z usług Salesforce do obiektów Blob platformy Azure](#json-example-copy-data-from-salesforce-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c8927-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c8927-134">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do usług Salesforce:</span><span class="sxs-lookup"><span data-stu-id="c8927-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="c8927-135">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="c8927-135">Linked service properties</span></span>
<span data-ttu-id="c8927-136">Poniższa tabela zawiera opisy elementów JSON, które są specyficzne dla usługi Salesforce połączone.</span><span class="sxs-lookup"><span data-stu-id="c8927-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="c8927-137">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c8927-137">Property</span></span> | <span data-ttu-id="c8927-138">Opis</span><span class="sxs-lookup"><span data-stu-id="c8927-138">Description</span></span> | <span data-ttu-id="c8927-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c8927-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8927-140">type</span><span class="sxs-lookup"><span data-stu-id="c8927-140">type</span></span> |<span data-ttu-id="c8927-141">Właściwość type musi mieć ustawioną: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c8927-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="c8927-142">Tak</span><span class="sxs-lookup"><span data-stu-id="c8927-142">Yes</span></span> |
| <span data-ttu-id="c8927-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="c8927-143">environmentUrl</span></span> | <span data-ttu-id="c8927-144">Określ wystąpienie adres URL usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c8927-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="c8927-145">-Domyślna to "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="c8927-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="c8927-146">-Aby skopiować dane z piaskownicy, określ "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="c8927-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="c8927-147">-Aby skopiować dane z domeny niestandardowej, określ, na przykład "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="c8927-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="c8927-148">Nie</span><span class="sxs-lookup"><span data-stu-id="c8927-148">No</span></span> |
| <span data-ttu-id="c8927-149">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="c8927-149">username</span></span> |<span data-ttu-id="c8927-150">Określ nazwę użytkownika dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8927-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="c8927-151">Tak</span><span class="sxs-lookup"><span data-stu-id="c8927-151">Yes</span></span> |
| <span data-ttu-id="c8927-152">hasło</span><span class="sxs-lookup"><span data-stu-id="c8927-152">password</span></span> |<span data-ttu-id="c8927-153">Określ hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8927-153">Specify a password for the user account.</span></span> |<span data-ttu-id="c8927-154">Tak</span><span class="sxs-lookup"><span data-stu-id="c8927-154">Yes</span></span> |
| <span data-ttu-id="c8927-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="c8927-155">securityToken</span></span> |<span data-ttu-id="c8927-156">Określ tokenu zabezpieczającego dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8927-156">Specify a security token for the user account.</span></span> <span data-ttu-id="c8927-157">Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje dotyczące resetowania/Get tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="c8927-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="c8927-158">Aby dowiedzieć się więcej o tokeny zabezpieczające ogólnie rzecz biorąc, zobacz [zabezpieczeń i interfejsu API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="c8927-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="c8927-159">Tak</span><span class="sxs-lookup"><span data-stu-id="c8927-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c8927-160">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c8927-160">Dataset properties</span></span>
<span data-ttu-id="c8927-161">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c8927-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c8927-162">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, tabeli platformy Azure i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="c8927-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="c8927-163">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="c8927-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c8927-164">TypeProperties sekcja dla zestawu danych typu **RelationalTable** ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="c8927-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="c8927-165">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c8927-165">Property</span></span> | <span data-ttu-id="c8927-166">Opis</span><span class="sxs-lookup"><span data-stu-id="c8927-166">Description</span></span> | <span data-ttu-id="c8927-167">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c8927-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8927-168">tableName</span><span class="sxs-lookup"><span data-stu-id="c8927-168">tableName</span></span> |<span data-ttu-id="c8927-169">Nazwa tabeli w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c8927-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="c8927-170">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="c8927-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c8927-171">Część "__c" Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="c8927-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="c8927-173">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="c8927-173">Copy activity properties</span></span>
<span data-ttu-id="c8927-174">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c8927-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c8927-175">Właściwości, takie jak tabele nazwę, opis, danych wejściowych i wyjściowych i różnych zasad są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="c8927-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="c8927-176">Właściwości, które są dostępne w sekcji typeProperties działania z drugiej strony, zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="c8927-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="c8927-177">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="c8927-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c8927-178">W przypadku działania kopiowania, gdy źródłem jest typu **RelationalSource** (która obejmuje usługi Salesforce), w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="c8927-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c8927-179">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c8927-179">Property</span></span> | <span data-ttu-id="c8927-180">Opis</span><span class="sxs-lookup"><span data-stu-id="c8927-180">Description</span></span> | <span data-ttu-id="c8927-181">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="c8927-181">Allowed values</span></span> | <span data-ttu-id="c8927-182">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c8927-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c8927-183">query</span><span class="sxs-lookup"><span data-stu-id="c8927-183">query</span></span> |<span data-ttu-id="c8927-184">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="c8927-184">Use the custom query to read data.</span></span> |<span data-ttu-id="c8927-185">Zapytania SQL 92 lub [Salesforce obiektu Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) zapytania.</span><span class="sxs-lookup"><span data-stu-id="c8927-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="c8927-186">Przykład: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="c8927-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="c8927-187">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="c8927-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c8927-188">Część "__c" Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="c8927-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="c8927-190">Wskazówki zapytania</span><span class="sxs-lookup"><span data-stu-id="c8927-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="c8927-191">Podczas pobierania danych przy użyciu where klauzuli według kolumny daty i godziny</span><span class="sxs-lookup"><span data-stu-id="c8927-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="c8927-192">Gdy Określ SOQL lub SQL zapytanie, zwrócić uwagę różnica format daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="c8927-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="c8927-193">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c8927-193">For example:</span></span>

* <span data-ttu-id="c8927-194">**Przykładowe SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c8927-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="c8927-195">**Przykładowe SQL**:</span><span class="sxs-lookup"><span data-stu-id="c8927-195">**SQL sample**:</span></span>
    * <span data-ttu-id="c8927-196">**Określ zapytanie za pomocą Kreatora kopiowania:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c8927-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="c8927-197">**Za pomocą edycji, aby określić zapytanie JSON (prawidłowo ucieczki znaku):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="c8927-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="c8927-198">Pobieranie danych z raportu usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="c8927-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="c8927-199">Można pobrać dane z raportów usług Salesforce, określając kwerendy w postaci `{call "<report name>"}`, na przykład.</span><span class="sxs-lookup"><span data-stu-id="c8927-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="c8927-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="c8927-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="c8927-201">Przywracanie usuniętych rekordów z Kosza usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="c8927-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="c8927-202">Kwerenda nietrwałego usuniętych rekordów z Kosza usług Salesforce, można określić **"IsDeleted = 1"** w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="c8927-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="c8927-203">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c8927-203">For example,</span></span>

* <span data-ttu-id="c8927-204">Aby odpytać tylko usunięte rekordy, określ "Wybierz * z MyTable__c **gdzie IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="c8927-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="c8927-205">Aby wysyłać zapytania o wszystkie rekordy tym usuniętych i istniejących, określ "Wybierz * z MyTable__c **gdzie IsDeleted = 0 lub IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="c8927-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="c8927-206">Przykład JSON: kopiowanie danych z usług Salesforce do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c8927-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="c8927-207">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c8927-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c8927-208">Przedstawiają sposób kopiowania danych z usług Salesforce do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="c8927-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="c8927-209">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c8927-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="c8927-210">Poniżej przedstawiono artefakty fabryki danych, które należy utworzyć w celu zaimplementowania scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c8927-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="c8927-211">Sekcje listy zawierają szczegółowe informacje na temat tych kroków.</span><span class="sxs-lookup"><span data-stu-id="c8927-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="c8927-212">Połączonej usługi typu [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c8927-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="c8927-213">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c8927-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="c8927-214">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c8927-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="c8927-215">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c8927-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="c8927-216">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="c8927-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="c8927-217">**Usługa SalesForce połączone**</span><span class="sxs-lookup"><span data-stu-id="c8927-217">**Salesforce linked service**</span></span>

<span data-ttu-id="c8927-218">W tym przykładzie użyto **Salesforce** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="c8927-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="c8927-219">Zobacz [Salesforce połączona usługa](#linked-service-properties) sekcję właściwości, które są obsługiwane przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="c8927-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="c8927-220">Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje dotyczące resetowania/Get tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="c8927-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="c8927-221">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="c8927-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="c8927-222">**Wejściowy zestaw danych usług SalesForce**</span><span class="sxs-lookup"><span data-stu-id="c8927-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
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

<span data-ttu-id="c8927-223">Ustawienie **zewnętrznych** do **true** usługi fabryka danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="c8927-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8927-224">Część "__c" Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="c8927-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="c8927-226">**Wyjściowy zestaw danych obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="c8927-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="c8927-227">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="c8927-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c8927-228">**Potok wraz z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="c8927-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="c8927-229">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="c8927-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="c8927-230">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource**i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c8927-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="c8927-231">Zobacz [właściwości typu RelationalSource](#copy-activity-properties) listę właściwości, które są obsługiwane przez RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="c8927-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="c8927-232">Część "__c" Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="c8927-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="c8927-234">Mapowanie typu dla usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="c8927-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="c8927-235">Typ usług SalesForce</span><span class="sxs-lookup"><span data-stu-id="c8927-235">Salesforce type</span></span> | <span data-ttu-id="c8927-236">. Typ opartej na sieci</span><span class="sxs-lookup"><span data-stu-id="c8927-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="c8927-237">Automatyczny numer</span><span class="sxs-lookup"><span data-stu-id="c8927-237">Auto Number</span></span> |<span data-ttu-id="c8927-238">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-238">String</span></span> |
| <span data-ttu-id="c8927-239">Pole wyboru</span><span class="sxs-lookup"><span data-stu-id="c8927-239">Checkbox</span></span> |<span data-ttu-id="c8927-240">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="c8927-240">Boolean</span></span> |
| <span data-ttu-id="c8927-241">Waluta</span><span class="sxs-lookup"><span data-stu-id="c8927-241">Currency</span></span> |<span data-ttu-id="c8927-242">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c8927-242">Double</span></span> |
| <span data-ttu-id="c8927-243">Date</span><span class="sxs-lookup"><span data-stu-id="c8927-243">Date</span></span> |<span data-ttu-id="c8927-244">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c8927-244">DateTime</span></span> |
| <span data-ttu-id="c8927-245">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c8927-245">Date/Time</span></span> |<span data-ttu-id="c8927-246">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c8927-246">DateTime</span></span> |
| <span data-ttu-id="c8927-247">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="c8927-247">Email</span></span> |<span data-ttu-id="c8927-248">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-248">String</span></span> |
| <span data-ttu-id="c8927-249">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="c8927-249">Id</span></span> |<span data-ttu-id="c8927-250">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-250">String</span></span> |
| <span data-ttu-id="c8927-251">Relacja wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="c8927-251">Lookup Relationship</span></span> |<span data-ttu-id="c8927-252">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-252">String</span></span> |
| <span data-ttu-id="c8927-253">Lista wyboru wielokrotnego wyboru</span><span class="sxs-lookup"><span data-stu-id="c8927-253">Multi-Select Picklist</span></span> |<span data-ttu-id="c8927-254">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-254">String</span></span> |
| <span data-ttu-id="c8927-255">Numer</span><span class="sxs-lookup"><span data-stu-id="c8927-255">Number</span></span> |<span data-ttu-id="c8927-256">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c8927-256">Double</span></span> |
| <span data-ttu-id="c8927-257">Procent</span><span class="sxs-lookup"><span data-stu-id="c8927-257">Percent</span></span> |<span data-ttu-id="c8927-258">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="c8927-258">Double</span></span> |
| <span data-ttu-id="c8927-259">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="c8927-259">Phone</span></span> |<span data-ttu-id="c8927-260">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-260">String</span></span> |
| <span data-ttu-id="c8927-261">Lista wyboru</span><span class="sxs-lookup"><span data-stu-id="c8927-261">Picklist</span></span> |<span data-ttu-id="c8927-262">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-262">String</span></span> |
| <span data-ttu-id="c8927-263">Tekst</span><span class="sxs-lookup"><span data-stu-id="c8927-263">Text</span></span> |<span data-ttu-id="c8927-264">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-264">String</span></span> |
| <span data-ttu-id="c8927-265">Obszar tekstu</span><span class="sxs-lookup"><span data-stu-id="c8927-265">Text Area</span></span> |<span data-ttu-id="c8927-266">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-266">String</span></span> |
| <span data-ttu-id="c8927-267">Obszar tekstu (Liczba długa)</span><span class="sxs-lookup"><span data-stu-id="c8927-267">Text Area (Long)</span></span> |<span data-ttu-id="c8927-268">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-268">String</span></span> |
| <span data-ttu-id="c8927-269">Obszar tekstu (zaawansowana)</span><span class="sxs-lookup"><span data-stu-id="c8927-269">Text Area (Rich)</span></span> |<span data-ttu-id="c8927-270">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-270">String</span></span> |
| <span data-ttu-id="c8927-271">Tekst (zaszyfrowane)</span><span class="sxs-lookup"><span data-stu-id="c8927-271">Text (Encrypted)</span></span> |<span data-ttu-id="c8927-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-272">String</span></span> |
| <span data-ttu-id="c8927-273">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="c8927-273">URL</span></span> |<span data-ttu-id="c8927-274">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c8927-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="c8927-275">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c8927-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="c8927-276">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="c8927-276">Performance and tuning</span></span>
<span data-ttu-id="c8927-277">Zobacz [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="c8927-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
