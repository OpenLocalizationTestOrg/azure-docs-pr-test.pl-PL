---
title: "aaaCopy tooand danych z usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy tooand danych z usługi Data Lake Store przy użyciu fabryki danych Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="acb8b-103">Skopiuj tooand danych z usługi Data Lake Store przy użyciu fabryki danych</span><span class="sxs-lookup"><span data-stu-id="acb8b-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="acb8b-104">W tym artykule opisano sposób toouse działanie kopiowania w fabryce danych Azure toomove danych tooand z usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="acb8b-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykuł Omówienie przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="acb8b-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="acb8b-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="acb8b-106">Supported scenarios</span></span>
<span data-ttu-id="acb8b-107">Dane należy skopiować **z usługi Azure Data Lake Store** toohello po magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="acb8b-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="acb8b-108">Można skopiować danych z powitania po magazyny danych **tooAzure usługi Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="acb8b-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="acb8b-109">Przed utworzeniem potoku z działania kopiowania, należy utworzyć konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="acb8b-110">Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="acb8b-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="acb8b-111">Typy obsługiwane uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="acb8b-111">Supported authentication types</span></span>
<span data-ttu-id="acb8b-112">Łącznik usługi Data Lake Store Hello obsługuje następujące typy uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="acb8b-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="acb8b-113">Uwierzytelnianie jednostki usługi</span><span class="sxs-lookup"><span data-stu-id="acb8b-113">Service principal authentication</span></span>
* <span data-ttu-id="acb8b-114">Uwierzytelnianie użytkownika poświadczeń (OAuth)</span><span class="sxs-lookup"><span data-stu-id="acb8b-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="acb8b-115">Firma Microsoft zaleca korzystanie z uwierzytelniania głównej usługi, zwłaszcza w przypadku kopiowania danych zaplanowane.</span><span class="sxs-lookup"><span data-stu-id="acb8b-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="acb8b-116">Zachowanie wygaśnięcia tokenu może wystąpić przy użyciu uwierzytelniania poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="acb8b-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="acb8b-117">Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="acb8b-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="acb8b-118">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="acb8b-118">Get started</span></span>
<span data-ttu-id="acb8b-119">Można utworzyć potok z działania kopiowania, który przenosi dane z usługi Azure Data Lake Store za pomocą różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="acb8b-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="acb8b-120">Witaj najprostszy sposób toocreate danych toocopy potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="acb8b-121">Samouczek dotyczący tworzenia za pomocą Kreatora kopiowania hello potoku, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="acb8b-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="acb8b-122">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="acb8b-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="acb8b-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="acb8b-124">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="acb8b-125">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-125">Create a **data factory**.</span></span> <span data-ttu-id="acb8b-126">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="acb8b-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="acb8b-127">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="acb8b-128">Na przykład jeśli dane są kopiowane z tooan magazynu obiektów blob platformy Azure, Azure Data Lake Store, tworzenia dwóch toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour magazynu usługi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="acb8b-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="acb8b-129">Dla właściwości połączonej usługi, które są określone tooAzure usługi Data Lake Store, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="acb8b-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="acb8b-130">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="acb8b-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="acb8b-131">Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="acb8b-132">I utwórz inny zestaw danych toospecify hello folderu i ścieżce pliku w magazynie usługi Data Lake hello, który przechowuje dane hello skopiowane z magazynu obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="acb8b-133">Dla właściwości zestawu danych, które są określone tooAzure usługi Data Lake Store, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="acb8b-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="acb8b-134">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="acb8b-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="acb8b-135">W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i AzureDataLakeStoreSink jako zbiorniku dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="acb8b-136">Podobnie są kopiowane z usługi Azure Data Lake Store tooAzure magazynu obiektów Blob, należy użyć AzureDataLakeStoreSource i BlobSink w przypadku działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="acb8b-137">Dla właściwości działania kopiowania, które są określone tooAzure usługi Data Lake Store, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="acb8b-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="acb8b-138">Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="acb8b-139">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="acb8b-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="acb8b-140">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="acb8b-141">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z usługi Azure Data Lake Store, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="acb8b-142">Witaj następujące sekcje zawierają szczegółowe informacje o właściwościach JSON, które są używane toodefine fabryki danych jednostek określonych tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="acb8b-143">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="acb8b-143">Linked service properties</span></span>
<span data-ttu-id="acb8b-144">Połączona usługa łączy fabryki danych tooa magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="acb8b-145">Tworzenie połączonej usługi typu **AzureDataLakeStore** toolink fabrykę danych tooyour danych Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="acb8b-146">Witaj w poniższej tabeli opisano określonych usług tooData Lake Store połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="acb8b-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="acb8b-147">Można wybrać usługę podmiotu zabezpieczeń i uwierzytelniania poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="acb8b-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="acb8b-148">Właściwość</span><span class="sxs-lookup"><span data-stu-id="acb8b-148">Property</span></span> | <span data-ttu-id="acb8b-149">Opis</span><span class="sxs-lookup"><span data-stu-id="acb8b-149">Description</span></span> | <span data-ttu-id="acb8b-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="acb8b-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="acb8b-151">**Typ**</span><span class="sxs-lookup"><span data-stu-id="acb8b-151">**type**</span></span> | <span data-ttu-id="acb8b-152">zbyt należy ustawić właściwość typu Hello**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="acb8b-153">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-153">Yes</span></span> |
| <span data-ttu-id="acb8b-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="acb8b-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="acb8b-155">Informacje o hello konta usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="acb8b-156">Informacja ta ma jeden z następujących formatów hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` lub `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="acb8b-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="acb8b-157">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-157">Yes</span></span> |
| <span data-ttu-id="acb8b-158">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="acb8b-158">**subscriptionId**</span></span> | <span data-ttu-id="acb8b-159">Należy hello toowhich identyfikator subskrypcji platformy Azure konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="acb8b-160">Wymagany dla odbiorcy</span><span class="sxs-lookup"><span data-stu-id="acb8b-160">Required for sink</span></span> |
| <span data-ttu-id="acb8b-161">**grupy zasobów o nazwie**</span><span class="sxs-lookup"><span data-stu-id="acb8b-161">**resourceGroupName**</span></span> | <span data-ttu-id="acb8b-162">Należy zasobów platformy Azure grupy nazwa toowhich hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="acb8b-163">Wymagany dla odbiorcy</span><span class="sxs-lookup"><span data-stu-id="acb8b-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="acb8b-164">Uwierzytelnianie główna usługi (zalecane)</span><span class="sxs-lookup"><span data-stu-id="acb8b-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="acb8b-165">główne uwierzytelnianie usługi toouse rejestru jednostki aplikacji w usłudze Azure Active Directory (Azure AD) i udziel go hello dostępu tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="acb8b-166">Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="acb8b-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="acb8b-167">Zwróć uwagę na powitania następujące wartości, których używasz toodefine hello połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="acb8b-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="acb8b-168">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="acb8b-168">Application ID</span></span>
* <span data-ttu-id="acb8b-169">Klucz aplikacji</span><span class="sxs-lookup"><span data-stu-id="acb8b-169">Application key</span></span> 
* <span data-ttu-id="acb8b-170">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="acb8b-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acb8b-171">Jeśli używasz hello kreatora kopiowania tooauthor danych potoki, upewnij się, przyznanie nazwy głównej usługi hello co najmniej **czytnika** roli w kontroli dostępu (Zarządzanie tożsamościami i dostępem) dla konta usługi Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="acb8b-172">Ponadto udzielić co najmniej nazwy głównej usługi hello **Odczyt i wykonywanie** głównym usługi Data Lake Store tooyour uprawnień ("/") i jej funkcji podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="acb8b-173">W przeciwnym razie można napotkać wiadomości powitania "hello, podane poświadczenia są nieprawidłowe."</span><span class="sxs-lookup"><span data-stu-id="acb8b-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="acb8b-174">Po utworzeniu lub zaktualizować nazwy głównej usługi w usłudze Azure AD, może upłynąć kilka minut, aż hello zmiany tootake efekt.</span><span class="sxs-lookup"><span data-stu-id="acb8b-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="acb8b-175">Sprawdź nazwę główną usługi hello i konfiguracjami listę kontroli dostępu (ACL) kontroli dostępu do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="acb8b-176">Jeśli widzisz nadal wiadomości powitania "hello, podane poświadczenia są nieprawidłowe", zaczekaj chwilę i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="acb8b-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="acb8b-177">Uwierzytelnianie usługi głównej określając hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="acb8b-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="acb8b-178">Właściwość</span><span class="sxs-lookup"><span data-stu-id="acb8b-178">Property</span></span> | <span data-ttu-id="acb8b-179">Opis</span><span class="sxs-lookup"><span data-stu-id="acb8b-179">Description</span></span> | <span data-ttu-id="acb8b-180">Wymagane</span><span class="sxs-lookup"><span data-stu-id="acb8b-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="acb8b-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="acb8b-181">**servicePrincipalId**</span></span> | <span data-ttu-id="acb8b-182">Określ identyfikator aplikacji hello klienta.</span><span class="sxs-lookup"><span data-stu-id="acb8b-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="acb8b-183">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-183">Yes</span></span> |
| <span data-ttu-id="acb8b-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="acb8b-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="acb8b-185">Określ klucz aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-185">Specify hello application's key.</span></span> | <span data-ttu-id="acb8b-186">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-186">Yes</span></span> |
| <span data-ttu-id="acb8b-187">**dzierżawy**</span><span class="sxs-lookup"><span data-stu-id="acb8b-187">**tenant**</span></span> | <span data-ttu-id="acb8b-188">Określ informacje dzierżawy hello (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja.</span><span class="sxs-lookup"><span data-stu-id="acb8b-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="acb8b-189">Można go pobrać aktywowania hello myszy w prawym górnym narożniku hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="acb8b-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="acb8b-190">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-190">Yes</span></span> |

<span data-ttu-id="acb8b-191">**Przykład: Usługa podmiotu zabezpieczeń uwierzytelniania**</span><span class="sxs-lookup"><span data-stu-id="acb8b-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="acb8b-192">Uwierzytelnianie poświadczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="acb8b-192">User credential authentication</span></span>
<span data-ttu-id="acb8b-193">Alternatywnie można użyć toocopy uwierzytelniania poświadczeń użytkownika z lub tooData Lake Store, określając hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="acb8b-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="acb8b-194">Właściwość</span><span class="sxs-lookup"><span data-stu-id="acb8b-194">Property</span></span> | <span data-ttu-id="acb8b-195">Opis</span><span class="sxs-lookup"><span data-stu-id="acb8b-195">Description</span></span> | <span data-ttu-id="acb8b-196">Wymagane</span><span class="sxs-lookup"><span data-stu-id="acb8b-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="acb8b-197">**autoryzacji**</span><span class="sxs-lookup"><span data-stu-id="acb8b-197">**authorization**</span></span> | <span data-ttu-id="acb8b-198">Kliknij przycisk hello **autoryzacji** przycisku na powitania Edytor fabryki danych i wprowadź Twoje poświadczenia przypisującej właściwość toothis hello wygenerowana automatycznie autoryzacji URL.</span><span class="sxs-lookup"><span data-stu-id="acb8b-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="acb8b-199">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-199">Yes</span></span> |
| <span data-ttu-id="acb8b-200">**Identyfikator sesji**</span><span class="sxs-lookup"><span data-stu-id="acb8b-200">**sessionId**</span></span> | <span data-ttu-id="acb8b-201">Identyfikator sesji OAuth z sesji autoryzacji OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="acb8b-202">Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="acb8b-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="acb8b-203">To ustawienie jest automatycznie generowany, gdy używasz hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="acb8b-204">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-204">Yes</span></span> |

<span data-ttu-id="acb8b-205">**Przykład: Użytkownik poświadczeń uwierzytelniania**</span><span class="sxs-lookup"><span data-stu-id="acb8b-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="acb8b-206">Wygaśnięcia tokenu</span><span class="sxs-lookup"><span data-stu-id="acb8b-206">Token expiration</span></span>
<span data-ttu-id="acb8b-207">Witaj kod autoryzacji, który generuje za pomocą hello **autoryzacji** przycisk wygasa po określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="acb8b-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="acb8b-208">następujące wiadomość Hello oznacza, że wygasł token uwierzytelniania hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="acb8b-209">Poświadczeń błąd operacji: invalid_grant - AADSTS70002: błąd podczas sprawdzania poprawności poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="acb8b-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="acb8b-210">AADSTS70008: hello podać Udziel dostępu jest wygasnąć lub zostać odwołane.</span><span class="sxs-lookup"><span data-stu-id="acb8b-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="acb8b-211">Identyfikator śledzenia: Identyfikator korelacji d18629e8-af88-43c5-88e3-d8419eb1fca1: sygnatura czasowa fac30a0c-6be6-4e02-8d69-a776d2ffefd7: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="acb8b-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="acb8b-212">Witaj poniższej tabeli przedstawiono czas wygaśnięcia hello różnych typów kont użytkowników:</span><span class="sxs-lookup"><span data-stu-id="acb8b-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="acb8b-213">Typ użytkownika</span><span class="sxs-lookup"><span data-stu-id="acb8b-213">User type</span></span> | <span data-ttu-id="acb8b-214">Wygasa po</span><span class="sxs-lookup"><span data-stu-id="acb8b-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="acb8b-215">Konta użytkowników *nie* zarządzane przez usługę Azure Active Directory (na przykład @hotmail.com lub @live.com)</span><span class="sxs-lookup"><span data-stu-id="acb8b-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="acb8b-216">12 godzin</span><span class="sxs-lookup"><span data-stu-id="acb8b-216">12 hours</span></span> |
| <span data-ttu-id="acb8b-217">Konta użytkowników zarządzanych przez usługę Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acb8b-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="acb8b-218">Uruchom 14 dni od ostatniego wycinek hello</span><span class="sxs-lookup"><span data-stu-id="acb8b-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="acb8b-219">90 dni, jeśli wycinek oparte na podstawie OAuth połączonej usługi jest uruchamiana co najmniej raz na 14 dni</span><span class="sxs-lookup"><span data-stu-id="acb8b-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="acb8b-220">Jeśli zmienisz hasło wcześniejszy niż czas wygaśnięcia tokenu hello hello token wygasa natychmiast.</span><span class="sxs-lookup"><span data-stu-id="acb8b-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="acb8b-221">Zostanie wyświetlony komunikat hello wymienione wcześniej w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="acb8b-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="acb8b-222">Można ponownie autoryzować hello konta przy użyciu hello **autoryzacji** przycisk wygaśnięcia tokenu hello tooredeploy hello połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="acb8b-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="acb8b-223">Można również tworzyć wartości hello **sessionId** i **autoryzacji** właściwości programowo przy użyciu hello następujący kod:</span><span class="sxs-lookup"><span data-stu-id="acb8b-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="acb8b-224">Aby uzyskać szczegółowe informacje o klasach fabryki danych hello używane w kodzie hello, zobacz hello [klasy AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [klasy AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), i [ Klasa AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tematów.</span><span class="sxs-lookup"><span data-stu-id="acb8b-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="acb8b-225">Dodaj tooversion odwołanie `2.9.10826.1824` z `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` dla hello `WindowsFormsWebAuthenticationDialog` klasa używana w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="acb8b-226">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="acb8b-226">Dataset properties</span></span>
<span data-ttu-id="acb8b-227">toospecify danych wejściowych toorepresent zestawu danych w usłudze Data Lake Store, ustaw hello **typu** właściwości zestawu danych hello zbyt**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="acb8b-228">Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello usługi Data Lake Store połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="acb8b-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="acb8b-229">Aby uzyskać pełną listę właściwości JSON sekcje i dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="acb8b-230">Sekcje zestawu danych w formacie JSON, takich jak **struktury**, **dostępności**, i **zasad**, są podobne dla wszystkich typów obiektów dataset (Azure SQL database, obiektów blob platformy Azure i tabeli platformy Azure, na przykład).</span><span class="sxs-lookup"><span data-stu-id="acb8b-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="acb8b-231">Witaj **typeProperties** sekcja zawiera informacje, takie jak lokalizacja i format hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="acb8b-232">Witaj **typeProperties** sekcja dla zestawu danych typu **AzureDataLakeStore** zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="acb8b-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="acb8b-233">Właściwość</span><span class="sxs-lookup"><span data-stu-id="acb8b-233">Property</span></span> | <span data-ttu-id="acb8b-234">Opis</span><span class="sxs-lookup"><span data-stu-id="acb8b-234">Description</span></span> | <span data-ttu-id="acb8b-235">Wymagane</span><span class="sxs-lookup"><span data-stu-id="acb8b-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="acb8b-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="acb8b-236">**folderPath**</span></span> |<span data-ttu-id="acb8b-237">Ścieżka toohello kontenera i folderu w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="acb8b-238">Tak</span><span class="sxs-lookup"><span data-stu-id="acb8b-238">Yes</span></span> |
| <span data-ttu-id="acb8b-239">**Nazwa pliku**</span><span class="sxs-lookup"><span data-stu-id="acb8b-239">**fileName**</span></span> |<span data-ttu-id="acb8b-240">Nazwa pliku hello w usłudze Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="acb8b-241">Witaj **fileName** właściwość jest opcjonalna i z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="acb8b-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="acb8b-242">Jeśli określisz **fileName**, hello działania (w tym kopiowania) działa na powitania określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="acb8b-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="acb8b-243">Gdy **fileName** nie zostanie określony, kopia zawiera wszystkie pliki w **folderPath** hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="acb8b-244">Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania hello hello wygenerowany plik nosi nazwę w formacie hello danych. _Identyfikator GUID_txt ".</span><span class="sxs-lookup"><span data-stu-id="acb8b-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="acb8b-245">Na przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="acb8b-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="acb8b-246">Nie</span><span class="sxs-lookup"><span data-stu-id="acb8b-246">No</span></span> |
| <span data-ttu-id="acb8b-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="acb8b-247">**partitionedBy**</span></span> |<span data-ttu-id="acb8b-248">Witaj **partitionedBy** właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="acb8b-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="acb8b-249">Służy on toospecify dynamiczne ścieżkę i nazwę pliku dla dane szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="acb8b-250">Na przykład **folderPath** mogą nadać parametry dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="acb8b-251">Aby uzyskać szczegółowe informacje i przykłady, zobacz [hello właściwości partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="acb8b-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="acb8b-252">Nie</span><span class="sxs-lookup"><span data-stu-id="acb8b-252">No</span></span> |
| <span data-ttu-id="acb8b-253">**Format**</span><span class="sxs-lookup"><span data-stu-id="acb8b-253">**format**</span></span> | <span data-ttu-id="acb8b-254">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, i  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="acb8b-255">Zestaw hello **typu** właściwości w **format** tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="acb8b-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="acb8b-256">Aby uzyskać więcej informacji, zobacz hello [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) części hello [formatów plików i ich kompresji, obsługiwanych przez usługi fabryka danych Azure](data-factory-supported-file-and-compression-formats.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="acb8b-257">Pliki toocopy "jako — jest" między opartych na plikach magazynów (kopia binarnego), Pomiń hello `format` sekcji w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="acb8b-258">Nie</span><span class="sxs-lookup"><span data-stu-id="acb8b-258">No</span></span> |
| <span data-ttu-id="acb8b-259">**Kompresja**</span><span class="sxs-lookup"><span data-stu-id="acb8b-259">**compression**</span></span> | <span data-ttu-id="acb8b-260">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="acb8b-261">Obsługiwane typy to **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="acb8b-262">Obsługiwane poziomy są **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="acb8b-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="acb8b-263">Aby uzyskać więcej informacji, zobacz [formatów plików i ich kompresji, obsługiwanych przez usługi fabryka danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="acb8b-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="acb8b-264">Nie</span><span class="sxs-lookup"><span data-stu-id="acb8b-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="acb8b-265">Właściwość partitionedBy Hello</span><span class="sxs-lookup"><span data-stu-id="acb8b-265">hello partitionedBy property</span></span>
<span data-ttu-id="acb8b-266">Można określić dynamiczne **folderPath** i **fileName** właściwości dane szeregów czasowych z hello **partitionedBy** właściwości, funkcje fabryki danych i systemu zmienne.</span><span class="sxs-lookup"><span data-stu-id="acb8b-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="acb8b-267">Aby uzyskać więcej informacji, zobacz hello [fabryki danych Azure — funkcje i zmienne systemu](data-factory-functions-variables.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="acb8b-268">W hello poniższy przykład `{Slice}` zostanie zastąpiona wartością hello hello fabryki danych systemu zmiennej `SliceStart` w formacie hello określonym (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="acb8b-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="acb8b-269">Nazwa Hello `SliceStart` odwołuje się czas rozpoczęcia toohello hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="acb8b-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="acb8b-270">Witaj `folderPath` właściwość jest różne dla każdego wycinka jako w `wikidatagateway/wikisampledataout/2014100103` lub `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="acb8b-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="acb8b-271">W powitania po przykład, hello rok, miesiąc, dzień i czas `SliceStart` są wyodrębniane do oddzielnych zmiennych, które są używane przez hello `folderPath` i `fileName` właściwości:</span><span class="sxs-lookup"><span data-stu-id="acb8b-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="acb8b-272">Więcej szczegółów na zestawy danych szeregu czasowego, planowania i wycinków, zobacz hello [zestawów danych w fabryce danych Azure](data-factory-create-datasets.md) i [fabryki danych planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="acb8b-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="acb8b-273">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="acb8b-273">Copy activity properties</span></span>
<span data-ttu-id="acb8b-274">Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="acb8b-275">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="acb8b-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="acb8b-276">Witaj właściwości dostępne w hello **typeProperties** sekcji działanie zależy od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="acb8b-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="acb8b-277">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="acb8b-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="acb8b-278">**AzureDataLakeStoreSource** obsługuje następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="acb8b-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="acb8b-279">Właściwość</span><span class="sxs-lookup"><span data-stu-id="acb8b-279">Property</span></span> | <span data-ttu-id="acb8b-280">Opis</span><span class="sxs-lookup"><span data-stu-id="acb8b-280">Description</span></span> | <span data-ttu-id="acb8b-281">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="acb8b-281">Allowed values</span></span> | <span data-ttu-id="acb8b-282">Wymagane</span><span class="sxs-lookup"><span data-stu-id="acb8b-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="acb8b-283">**cykliczne**</span><span class="sxs-lookup"><span data-stu-id="acb8b-283">**recursive**</span></span> |<span data-ttu-id="acb8b-284">Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="acb8b-285">TRUE, False (wartość domyślna)</span><span class="sxs-lookup"><span data-stu-id="acb8b-285">True (default value), False</span></span> |<span data-ttu-id="acb8b-286">Nie</span><span class="sxs-lookup"><span data-stu-id="acb8b-286">No</span></span> |


<span data-ttu-id="acb8b-287">**AzureDataLakeStoreSink** obsługuje następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="acb8b-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="acb8b-288">Właściwość</span><span class="sxs-lookup"><span data-stu-id="acb8b-288">Property</span></span> | <span data-ttu-id="acb8b-289">Opis</span><span class="sxs-lookup"><span data-stu-id="acb8b-289">Description</span></span> | <span data-ttu-id="acb8b-290">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="acb8b-290">Allowed values</span></span> | <span data-ttu-id="acb8b-291">Wymagane</span><span class="sxs-lookup"><span data-stu-id="acb8b-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="acb8b-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="acb8b-292">**copyBehavior**</span></span> |<span data-ttu-id="acb8b-293">Określa zachowanie kopii hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="acb8b-294"><b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="acb8b-295">Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.</span><span class="sxs-lookup"><span data-stu-id="acb8b-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="acb8b-296"><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom hello folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="acb8b-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="acb8b-297">pliki docelowe Hello są tworzone z nazwami wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="acb8b-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="acb8b-298"><b>MergeFiles</b>: scala wszystkie pliki z pliku tooone folderu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="acb8b-299">Witaj nazwę pliku lub obiektu blob jest określony, nazwa scalony plik hello będzie hello określonej nazwy.</span><span class="sxs-lookup"><span data-stu-id="acb8b-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="acb8b-300">W przeciwnym razie hello nazwa pliku zostanie wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="acb8b-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="acb8b-301">Nie</span><span class="sxs-lookup"><span data-stu-id="acb8b-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="acb8b-302">Przykłady cyklicznego i copyBehavior</span><span class="sxs-lookup"><span data-stu-id="acb8b-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="acb8b-303">W tej sekcji opisano hello efekty hello operacji kopiowania dla różnych kombinacji wartości cyklicznej i copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="acb8b-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="acb8b-304">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="acb8b-304">recursive</span></span> | <span data-ttu-id="acb8b-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="acb8b-305">copyBehavior</span></span> | <span data-ttu-id="acb8b-306">Efekty</span><span class="sxs-lookup"><span data-stu-id="acb8b-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="acb8b-307">Wartość true</span><span class="sxs-lookup"><span data-stu-id="acb8b-307">true</span></span> |<span data-ttu-id="acb8b-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="acb8b-308">preserveHierarchy</span></span> |<span data-ttu-id="acb8b-309">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="acb8b-310">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-310">Folder1</span></span><br/><span data-ttu-id="acb8b-311">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-312">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="acb8b-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="acb8b-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="acb8b-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="acb8b-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="acb8b-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="acb8b-317">folder docelowy Hello Folder1 jest tworzony z hello takie same struktury jako źródło hello</span><span class="sxs-lookup"><span data-stu-id="acb8b-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="acb8b-318">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-318">Folder1</span></span><br/><span data-ttu-id="acb8b-319">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-320">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="acb8b-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="acb8b-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="acb8b-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="acb8b-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="acb8b-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="acb8b-325">Wartość true</span><span class="sxs-lookup"><span data-stu-id="acb8b-325">true</span></span> |<span data-ttu-id="acb8b-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="acb8b-326">flattenHierarchy</span></span> |<span data-ttu-id="acb8b-327">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="acb8b-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-328">Folder1</span></span><br/><span data-ttu-id="acb8b-329">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-330">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="acb8b-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="acb8b-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="acb8b-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="acb8b-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="acb8b-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="acb8b-335">docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="acb8b-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-336">Folder1</span></span><br/><span data-ttu-id="acb8b-337">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="acb8b-338">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="acb8b-339">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="acb8b-340">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="acb8b-341">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5</span><span class="sxs-lookup"><span data-stu-id="acb8b-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="acb8b-342">Wartość true</span><span class="sxs-lookup"><span data-stu-id="acb8b-342">true</span></span> |<span data-ttu-id="acb8b-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="acb8b-343">mergeFiles</span></span> |<span data-ttu-id="acb8b-344">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="acb8b-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-345">Folder1</span></span><br/><span data-ttu-id="acb8b-346">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-347">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="acb8b-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="acb8b-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="acb8b-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="acb8b-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="acb8b-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="acb8b-352">docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="acb8b-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-353">Folder1</span></span><br/><span data-ttu-id="acb8b-354">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie generowanych automatycznie</span><span class="sxs-lookup"><span data-stu-id="acb8b-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="acb8b-355">wartość false</span><span class="sxs-lookup"><span data-stu-id="acb8b-355">false</span></span> |<span data-ttu-id="acb8b-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="acb8b-356">preserveHierarchy</span></span> |<span data-ttu-id="acb8b-357">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="acb8b-358">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-358">Folder1</span></span><br/><span data-ttu-id="acb8b-359">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-360">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="acb8b-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="acb8b-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="acb8b-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="acb8b-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="acb8b-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="acb8b-365">folder docelowy Hello Folder1 jest tworzony z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="acb8b-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="acb8b-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-366">Folder1</span></span><br/><span data-ttu-id="acb8b-367">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-368">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="acb8b-369">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="acb8b-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="acb8b-370">wartość false</span><span class="sxs-lookup"><span data-stu-id="acb8b-370">false</span></span> |<span data-ttu-id="acb8b-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="acb8b-371">flattenHierarchy</span></span> |<span data-ttu-id="acb8b-372">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="acb8b-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-373">Folder1</span></span><br/><span data-ttu-id="acb8b-374">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-375">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="acb8b-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="acb8b-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="acb8b-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="acb8b-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="acb8b-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="acb8b-380">folder docelowy Hello Folder1 jest tworzony z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="acb8b-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="acb8b-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-381">Folder1</span></span><br/><span data-ttu-id="acb8b-382">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="acb8b-383">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="acb8b-384">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="acb8b-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="acb8b-385">wartość false</span><span class="sxs-lookup"><span data-stu-id="acb8b-385">false</span></span> |<span data-ttu-id="acb8b-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="acb8b-386">mergeFiles</span></span> |<span data-ttu-id="acb8b-387">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="acb8b-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="acb8b-388">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-388">Folder1</span></span><br/><span data-ttu-id="acb8b-389">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="acb8b-390">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="acb8b-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="acb8b-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="acb8b-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="acb8b-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="acb8b-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="acb8b-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="acb8b-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="acb8b-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="acb8b-395">folder docelowy Hello Folder1 jest tworzony z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="acb8b-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="acb8b-396">Folder1</span><span class="sxs-lookup"><span data-stu-id="acb8b-396">Folder1</span></span><br/><span data-ttu-id="acb8b-397">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="acb8b-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="acb8b-398">Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="acb8b-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="acb8b-399">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="acb8b-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="acb8b-400">Obsługiwane formaty plików i kompresji</span><span class="sxs-lookup"><span data-stu-id="acb8b-400">Supported file and compression formats</span></span>
<span data-ttu-id="acb8b-401">Aby uzyskać więcej informacji, zobacz hello [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="acb8b-402">Przykłady JSON kopiowania tooand danych z usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="acb8b-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="acb8b-403">Następujące przykłady Hello zawierają definicje JSON.</span><span class="sxs-lookup"><span data-stu-id="acb8b-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="acb8b-404">Te przykładowe definicje toocreate potoku można użyć przy użyciu hello [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="acb8b-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="acb8b-405">Witaj przykładach pokazano, jak toocopy tooand danych z magazynu usługi Data Lake Store i obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="acb8b-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="acb8b-406">Jednak dane mogą być kopiowane _bezpośrednio_ za pomocą dowolnego hello tooany źródeł z wychwytywanie hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="acb8b-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="acb8b-407">Aby uzyskać więcej informacji, zobacz sekcja hello "obsługiwane magazyny danych i formaty" w hello [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="acb8b-408">Przykład: Kopiowanie danych z magazynu obiektów Blob Azure tooAzure usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="acb8b-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="acb8b-409">Witaj przykładowy kod w tej sekcji przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="acb8b-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="acb8b-410">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="acb8b-411">Połączonej usługi typu [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="acb8b-412">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="acb8b-413">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="acb8b-414">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="acb8b-415">Witaj przykładach pokazano, jak szeregów czasowych dane z magazynu obiektów Blob platformy Azure są kopiowane tooData Lake Store co godzinę.</span><span class="sxs-lookup"><span data-stu-id="acb8b-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="acb8b-416">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="acb8b-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="acb8b-417">**Azure Data Lake Store połączona usługa**</span><span class="sxs-lookup"><span data-stu-id="acb8b-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="acb8b-418">Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="acb8b-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="acb8b-419">**Wejściowy zestaw danych obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="acb8b-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="acb8b-420">W hello poniższy przykład, danych jest pobierana z obiektu blob nowe co godzinę (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="acb8b-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="acb8b-421">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="acb8b-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="acb8b-422">Ścieżka folderu Hello używa hello rok, miesiąc i dzień część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="acb8b-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="acb8b-423">Nazwa pliku Hello używa godzina hello część hello godzinę rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="acb8b-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="acb8b-424">Witaj `"external": true` ustawienie informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="acb8b-425">**Azure Data Lake Store wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="acb8b-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="acb8b-426">powitania po przykład kopii tooData usługi data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acb8b-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="acb8b-427">Nowe dane są kopiowane tooData Lake Store co godzinę.</span><span class="sxs-lookup"><span data-stu-id="acb8b-427">New data is copied tooData Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="acb8b-428">**Działanie kopiowania w potoku źródła obiektów blob i ujście usługi Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="acb8b-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="acb8b-429">Poniższy przykład hello, potoku hello zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="acb8b-430">działanie kopiowania Hello jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="acb8b-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="acb8b-431">W potoku hello definicji JSON, hello `source` typu ustawiono zbyt`BlobSource`i hello `sink` typu ustawiono zbyt`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="acb8b-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="acb8b-432">Przykład: Kopiowanie danych z usługi Azure Data Lake Store tooan obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="acb8b-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="acb8b-433">Witaj przykładowy kod w tej sekcji przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="acb8b-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="acb8b-434">Połączonej usługi typu [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="acb8b-435">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="acb8b-436">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="acb8b-437">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="acb8b-438">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [AzureDataLakeStoreSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="acb8b-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="acb8b-439">Kod Hello kopiuje dane szeregów czasowych z tooan Data Lake — magazyn obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="acb8b-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="acb8b-440">**Azure Data Lake Store połączona usługa**</span><span class="sxs-lookup"><span data-stu-id="acb8b-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="acb8b-441">Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="acb8b-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="acb8b-442">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="acb8b-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="acb8b-443">**Usługa Azure Data Lake wejściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="acb8b-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="acb8b-444">W tym przykładzie ustawienie `"external"` zbyt`true` informuje usługi fabryka danych hello tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="acb8b-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
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
<span data-ttu-id="acb8b-445">**Wyjściowy zestaw danych obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="acb8b-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="acb8b-446">W hello poniższy przykład, dane są zapisywane nowego obiektu blob tooa co godzinę (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="acb8b-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="acb8b-447">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="acb8b-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="acb8b-448">Ścieżka folderu Hello używa hello roku, miesiąc, dzień i godziny część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="acb8b-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="acb8b-449">**Działanie kopiowania w potoku ze źródłem Azure Data Lake Store i ujście obiektów blob**</span><span class="sxs-lookup"><span data-stu-id="acb8b-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="acb8b-450">Poniższy przykład hello, potoku hello zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="acb8b-451">działanie kopiowania Hello jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="acb8b-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="acb8b-452">W potoku hello definicji JSON, hello `source` typu ustawiono zbyt`AzureDataLakeStoreSource`i hello `sink` typu ustawiono zbyt`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="acb8b-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="acb8b-453">W definicji działania kopiowania hello można również mapować kolumn z powitania źródło zestawu danych toocolumns w zestawie hello ujścia danych.</span><span class="sxs-lookup"><span data-stu-id="acb8b-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="acb8b-454">Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="acb8b-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="acb8b-455">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="acb8b-455">Performance and tuning</span></span>
<span data-ttu-id="acb8b-456">toolearn czynniki hello, które mają wpływ na wydajność działania kopiowania i w jaki sposób toooptimize, zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="acb8b-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
