---
title: "aaaMove dane z witryny Salesforce przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o danych toomove z witryny Salesforce przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="36e39-103">Przenieść dane z witryny Salesforce przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="36e39-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="36e39-104">W tym artykule omówiono używania działania kopiowania danych toocopy fabryki danych Azure z magazynem danych tooany Salesforce, który znajduje się w kolumnie zbiornika hello w hello [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="36e39-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="36e39-105">W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z kombinacji magazynu obsługiwane dane i działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="36e39-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="36e39-106">Fabryka danych Azure aktualnie obsługuje tylko do przenoszenia danych z usług Salesforce za[obsługiwane magazyny danych zbiornika](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ale nie obsługuje przenoszenia danych z innych tooSalesforce magazynów danych.</span><span class="sxs-lookup"><span data-stu-id="36e39-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="36e39-107">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="36e39-107">Supported versions</span></span>
<span data-ttu-id="36e39-108">Ten łącznik obsługuje następujące wersje usług Salesforce hello: Developer Edition w wersji Professional, Enterprise Edition albo nieograniczone Edition.</span><span class="sxs-lookup"><span data-stu-id="36e39-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="36e39-109">I obsługuje kopiowanie z Salesforce produkcji, piaskownicy i domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="36e39-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36e39-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="36e39-110">Prerequisites</span></span>
* <span data-ttu-id="36e39-111">Musi być włączone uprawnienia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="36e39-111">API permission must be enabled.</span></span> <span data-ttu-id="36e39-112">Zobacz [jak włączyć dostęp do interfejsu API w usłudze Salesforce przez zestaw uprawnień?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="36e39-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="36e39-113">toocopy danych z baz danych lokalnych tooon Salesforce, użytkownik musi mieć co najmniej 2.0 bramy zarządzania danych zainstalowanej w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="36e39-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="36e39-114">Limity żądań usług SalesForce</span><span class="sxs-lookup"><span data-stu-id="36e39-114">Salesforce request limits</span></span>
<span data-ttu-id="36e39-115">Usługa SalesForce obejmuje limity dla całkowita liczba żądań interfejsu API i równoczesnych żądań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="36e39-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="36e39-116">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="36e39-116">Note hello following points:</span></span>

- <span data-ttu-id="36e39-117">Jeśli hello liczbę jednoczesnych żądań przekracza hello limit, ograniczanie występuje, i zobaczysz losowe awarie.</span><span class="sxs-lookup"><span data-stu-id="36e39-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="36e39-118">Jeśli hello całkowita liczba żądań przekracza hello limit, hello konta usług Salesforce jest blokowana przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="36e39-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="36e39-119">Może również wyświetlony błąd "REQUEST_LIMIT_EXCEEDED" hello, w obu przypadkach.</span><span class="sxs-lookup"><span data-stu-id="36e39-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="36e39-120">Sekcja hello "interfejsu API limity żądań" w hello [Salesforce Developer limity](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="36e39-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="36e39-121">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="36e39-121">Getting started</span></span>
<span data-ttu-id="36e39-122">Można utworzyć potok z działania kopiowania, który przenosi dane z witryny Salesforce przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="36e39-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="36e39-123">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="36e39-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="36e39-124">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="36e39-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="36e39-125">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager **, **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="36e39-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="36e39-126">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="36e39-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="36e39-127">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="36e39-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="36e39-128">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="36e39-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="36e39-129">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="36e39-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="36e39-130">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="36e39-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="36e39-131">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="36e39-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="36e39-132">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="36e39-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="36e39-133">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z usług Salesforce, zobacz [przykład JSON: kopiowanie danych z usług Salesforce tooAzure obiektu Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="36e39-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="36e39-134">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooSalesforce:</span><span class="sxs-lookup"><span data-stu-id="36e39-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="36e39-135">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="36e39-135">Linked service properties</span></span>
<span data-ttu-id="36e39-136">Hello w poniższej tabeli opisano elementy JSON, które są określone toohello Salesforce połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="36e39-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="36e39-137">Właściwość</span><span class="sxs-lookup"><span data-stu-id="36e39-137">Property</span></span> | <span data-ttu-id="36e39-138">Opis</span><span class="sxs-lookup"><span data-stu-id="36e39-138">Description</span></span> | <span data-ttu-id="36e39-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="36e39-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e39-140">type</span><span class="sxs-lookup"><span data-stu-id="36e39-140">type</span></span> |<span data-ttu-id="36e39-141">musi mieć ustawioną właściwość type Hello: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="36e39-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="36e39-142">Tak</span><span class="sxs-lookup"><span data-stu-id="36e39-142">Yes</span></span> |
| <span data-ttu-id="36e39-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="36e39-143">environmentUrl</span></span> | <span data-ttu-id="36e39-144">Określ wystąpienie adres URL usługi Salesforce hello.</span><span class="sxs-lookup"><span data-stu-id="36e39-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="36e39-145">-Domyślna to "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="36e39-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="36e39-146">-toocopy danych z piaskownicy, określ "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="36e39-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="36e39-147">-toocopy dane z domeny niestandardowej, określić, na przykład "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="36e39-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="36e39-148">Nie</span><span class="sxs-lookup"><span data-stu-id="36e39-148">No</span></span> |
| <span data-ttu-id="36e39-149">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="36e39-149">username</span></span> |<span data-ttu-id="36e39-150">Określ nazwę użytkownika dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="36e39-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="36e39-151">Tak</span><span class="sxs-lookup"><span data-stu-id="36e39-151">Yes</span></span> |
| <span data-ttu-id="36e39-152">hasło</span><span class="sxs-lookup"><span data-stu-id="36e39-152">password</span></span> |<span data-ttu-id="36e39-153">Określ hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="36e39-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="36e39-154">Tak</span><span class="sxs-lookup"><span data-stu-id="36e39-154">Yes</span></span> |
| <span data-ttu-id="36e39-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="36e39-155">securityToken</span></span> |<span data-ttu-id="36e39-156">Określ tokenu zabezpieczającego dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="36e39-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="36e39-157">Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje na temat tooreset/get tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="36e39-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="36e39-158">Ogólnie rzecz biorąc, zobacz toolearn o tokeny zabezpieczające [zabezpieczeń i hello interfejsu API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="36e39-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="36e39-159">Tak</span><span class="sxs-lookup"><span data-stu-id="36e39-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="36e39-160">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="36e39-160">Dataset properties</span></span>
<span data-ttu-id="36e39-161">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="36e39-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="36e39-162">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, tabeli platformy Azure i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="36e39-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="36e39-163">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="36e39-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="36e39-164">Witaj typeProperties sekcja dla zestawu danych typu hello **RelationalTable** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="36e39-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="36e39-165">Właściwość</span><span class="sxs-lookup"><span data-stu-id="36e39-165">Property</span></span> | <span data-ttu-id="36e39-166">Opis</span><span class="sxs-lookup"><span data-stu-id="36e39-166">Description</span></span> | <span data-ttu-id="36e39-167">Wymagane</span><span class="sxs-lookup"><span data-stu-id="36e39-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e39-168">tableName</span><span class="sxs-lookup"><span data-stu-id="36e39-168">tableName</span></span> |<span data-ttu-id="36e39-169">Nazwa tabeli hello w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="36e39-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="36e39-170">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="36e39-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="36e39-171">Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="36e39-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="36e39-173">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="36e39-173">Copy activity properties</span></span>
<span data-ttu-id="36e39-174">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="36e39-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="36e39-175">Właściwości, takie jak tabele nazwę, opis, danych wejściowych i wyjściowych i różnych zasad są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="36e39-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="36e39-176">Hello właściwości, które są dostępne w hello drugiej sekcji typeProperties aktywności hello na powitania, zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="36e39-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="36e39-177">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="36e39-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="36e39-178">W przypadku działania kopiowania, gdy źródłem hello jest typu hello **RelationalSource** (która obejmuje usługi Salesforce), hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="36e39-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="36e39-179">Właściwość</span><span class="sxs-lookup"><span data-stu-id="36e39-179">Property</span></span> | <span data-ttu-id="36e39-180">Opis</span><span class="sxs-lookup"><span data-stu-id="36e39-180">Description</span></span> | <span data-ttu-id="36e39-181">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="36e39-181">Allowed values</span></span> | <span data-ttu-id="36e39-182">Wymagane</span><span class="sxs-lookup"><span data-stu-id="36e39-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36e39-183">query</span><span class="sxs-lookup"><span data-stu-id="36e39-183">query</span></span> |<span data-ttu-id="36e39-184">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="36e39-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="36e39-185">Zapytania SQL 92 lub [Salesforce obiektu Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) zapytania.</span><span class="sxs-lookup"><span data-stu-id="36e39-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="36e39-186">Przykład: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="36e39-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="36e39-187">Nie (jeśli hello **tableName** z hello **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="36e39-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="36e39-188">Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="36e39-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="36e39-190">Wskazówki zapytania</span><span class="sxs-lookup"><span data-stu-id="36e39-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="36e39-191">Podczas pobierania danych przy użyciu where klauzuli według kolumny daty i godziny</span><span class="sxs-lookup"><span data-stu-id="36e39-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="36e39-192">Gdy Określ hello SOQL lub SQL zapytanie, płatności uwagi toohello różnica format daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="36e39-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="36e39-193">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36e39-193">For example:</span></span>

* <span data-ttu-id="36e39-194">**Przykładowe SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="36e39-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="36e39-195">**Przykładowe SQL**:</span><span class="sxs-lookup"><span data-stu-id="36e39-195">**SQL sample**:</span></span>
    * <span data-ttu-id="36e39-196">**Stosowanie zapytania hello toospecify kreatora kopiowania:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="36e39-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="36e39-197">**Przy użyciu edycji toospecify hello kwerendy (prawidłowo ucieczki znaku):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="36e39-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="36e39-198">Pobieranie danych z raportu usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="36e39-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="36e39-199">Można pobrać dane z raportów usług Salesforce, określając kwerendy w postaci `{call "<report name>"}`, na przykład.</span><span class="sxs-lookup"><span data-stu-id="36e39-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="36e39-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="36e39-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="36e39-201">Przywracanie usuniętych rekordów z Kosza usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="36e39-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="36e39-202">tooquery hello nietrwałego usunięte rekordy z Kosza usług Salesforce, można określić **"IsDeleted = 1"** w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="36e39-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="36e39-203">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36e39-203">For example,</span></span>

* <span data-ttu-id="36e39-204">Określ tooquery tylko usunięte hello rekordy "Wybierz * z MyTable__c **gdzie IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="36e39-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="36e39-205">tooquery hello wszystkich rekordów, łącznie z istniejących hello i hello usunięty, określ "Wybierz * z MyTable__c **gdzie IsDeleted = 0 lub IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="36e39-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="36e39-206">Przykład JSON: kopiowanie danych z usług Salesforce tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="36e39-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="36e39-207">Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu hello można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="36e39-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="36e39-208">Przedstawiają sposób toocopy dane usług Salesforce tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="36e39-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="36e39-209">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="36e39-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="36e39-210">Poniżej przedstawiono hello artefakty fabryki danych należy toocreate tooimplement hello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="36e39-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="36e39-211">sekcje Hello listy hello zawierają szczegółowe informacje na temat tych kroków.</span><span class="sxs-lookup"><span data-stu-id="36e39-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="36e39-212">Połączonej usługi typu hello [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="36e39-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="36e39-213">Połączonej usługi typu hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="36e39-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="36e39-214">Dane wejściowe [dataset](data-factory-create-datasets.md) typu hello [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="36e39-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="36e39-215">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="36e39-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="36e39-216">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="36e39-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="36e39-217">**Usługa SalesForce połączone**</span><span class="sxs-lookup"><span data-stu-id="36e39-217">**Salesforce linked service**</span></span>

<span data-ttu-id="36e39-218">W tym przykładzie użyto hello **Salesforce** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="36e39-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="36e39-219">Zobacz hello [Salesforce połączona usługa](#linked-service-properties) sekcji hello właściwości, które są obsługiwane przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="36e39-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="36e39-220">Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje dotyczące sposobu tooreset/get hello tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="36e39-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

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
<span data-ttu-id="36e39-221">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="36e39-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="36e39-222">**Wejściowy zestaw danych usług SalesForce**</span><span class="sxs-lookup"><span data-stu-id="36e39-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="36e39-223">Ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="36e39-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36e39-224">Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="36e39-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="36e39-226">**Wyjściowy zestaw danych obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="36e39-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="36e39-227">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="36e39-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="36e39-228">**Potok wraz z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="36e39-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="36e39-229">Witaj potoku zawiera działanie kopiowania, która jest skonfigurowana toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="36e39-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="36e39-230">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource**i hello **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="36e39-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="36e39-231">Zobacz [właściwości typu RelationalSource](#copy-activity-properties) hello listę właściwości, które są obsługiwane przez hello RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="36e39-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="36e39-232">Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="36e39-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Nazwa danych fabryki — połączenie usługi Salesforce — interfejs API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="36e39-234">Mapowanie typu dla usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="36e39-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="36e39-235">Typ usług SalesForce</span><span class="sxs-lookup"><span data-stu-id="36e39-235">Salesforce type</span></span> | <span data-ttu-id="36e39-236">. Typ opartej na sieci</span><span class="sxs-lookup"><span data-stu-id="36e39-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="36e39-237">Automatyczny numer</span><span class="sxs-lookup"><span data-stu-id="36e39-237">Auto Number</span></span> |<span data-ttu-id="36e39-238">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-238">String</span></span> |
| <span data-ttu-id="36e39-239">Pole wyboru</span><span class="sxs-lookup"><span data-stu-id="36e39-239">Checkbox</span></span> |<span data-ttu-id="36e39-240">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="36e39-240">Boolean</span></span> |
| <span data-ttu-id="36e39-241">Waluta</span><span class="sxs-lookup"><span data-stu-id="36e39-241">Currency</span></span> |<span data-ttu-id="36e39-242">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="36e39-242">Double</span></span> |
| <span data-ttu-id="36e39-243">Date</span><span class="sxs-lookup"><span data-stu-id="36e39-243">Date</span></span> |<span data-ttu-id="36e39-244">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="36e39-244">DateTime</span></span> |
| <span data-ttu-id="36e39-245">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="36e39-245">Date/Time</span></span> |<span data-ttu-id="36e39-246">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="36e39-246">DateTime</span></span> |
| <span data-ttu-id="36e39-247">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="36e39-247">Email</span></span> |<span data-ttu-id="36e39-248">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-248">String</span></span> |
| <span data-ttu-id="36e39-249">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="36e39-249">Id</span></span> |<span data-ttu-id="36e39-250">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-250">String</span></span> |
| <span data-ttu-id="36e39-251">Relacja wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="36e39-251">Lookup Relationship</span></span> |<span data-ttu-id="36e39-252">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-252">String</span></span> |
| <span data-ttu-id="36e39-253">Lista wyboru wielokrotnego wyboru</span><span class="sxs-lookup"><span data-stu-id="36e39-253">Multi-Select Picklist</span></span> |<span data-ttu-id="36e39-254">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-254">String</span></span> |
| <span data-ttu-id="36e39-255">Liczba</span><span class="sxs-lookup"><span data-stu-id="36e39-255">Number</span></span> |<span data-ttu-id="36e39-256">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="36e39-256">Double</span></span> |
| <span data-ttu-id="36e39-257">Procent</span><span class="sxs-lookup"><span data-stu-id="36e39-257">Percent</span></span> |<span data-ttu-id="36e39-258">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="36e39-258">Double</span></span> |
| <span data-ttu-id="36e39-259">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="36e39-259">Phone</span></span> |<span data-ttu-id="36e39-260">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-260">String</span></span> |
| <span data-ttu-id="36e39-261">Lista wyboru</span><span class="sxs-lookup"><span data-stu-id="36e39-261">Picklist</span></span> |<span data-ttu-id="36e39-262">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-262">String</span></span> |
| <span data-ttu-id="36e39-263">Tekst</span><span class="sxs-lookup"><span data-stu-id="36e39-263">Text</span></span> |<span data-ttu-id="36e39-264">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-264">String</span></span> |
| <span data-ttu-id="36e39-265">Obszar tekstu</span><span class="sxs-lookup"><span data-stu-id="36e39-265">Text Area</span></span> |<span data-ttu-id="36e39-266">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-266">String</span></span> |
| <span data-ttu-id="36e39-267">Obszar tekstu (Liczba długa)</span><span class="sxs-lookup"><span data-stu-id="36e39-267">Text Area (Long)</span></span> |<span data-ttu-id="36e39-268">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-268">String</span></span> |
| <span data-ttu-id="36e39-269">Obszar tekstu (zaawansowana)</span><span class="sxs-lookup"><span data-stu-id="36e39-269">Text Area (Rich)</span></span> |<span data-ttu-id="36e39-270">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-270">String</span></span> |
| <span data-ttu-id="36e39-271">Tekst (zaszyfrowane)</span><span class="sxs-lookup"><span data-stu-id="36e39-271">Text (Encrypted)</span></span> |<span data-ttu-id="36e39-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-272">String</span></span> |
| <span data-ttu-id="36e39-273">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="36e39-273">URL</span></span> |<span data-ttu-id="36e39-274">Ciąg</span><span class="sxs-lookup"><span data-stu-id="36e39-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="36e39-275">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="36e39-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="36e39-276">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="36e39-276">Performance and tuning</span></span>
<span data-ttu-id="36e39-277">Zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="36e39-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
