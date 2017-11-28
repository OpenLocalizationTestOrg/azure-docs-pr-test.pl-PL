---
title: "aaaTransform danych przy użyciu skryptu U-SQL - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprocess lub Przekształcanie danych za pomocą skryptów U-SQL w usłudze Azure Data Lake Analytics obliczeniowe usługi."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="389f7-103">Przekształcanie danych za pomocą skryptów U-SQL w usłudze Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="389f7-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="389f7-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="389f7-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="389f7-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="389f7-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="389f7-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="389f7-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="389f7-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="389f7-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="389f7-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="389f7-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="389f7-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="389f7-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="389f7-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="389f7-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="389f7-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="389f7-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="389f7-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="389f7-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="389f7-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="389f7-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="389f7-114">Potok w fabryce danych Azure przetwarza dane w usługach magazynu połączone, przy użyciu obliczeniowego połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="389f7-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="389f7-115">Zawiera sekwencję działań, gdzie każde działanie wykonuje operację przetwarzania specyficznego dla.</span><span class="sxs-lookup"><span data-stu-id="389f7-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="389f7-116">W tym artykule opisano hello **Data Lake Analytics U-SQL działania** , na którym działa **U-SQL** skryptom na **Azure Data Lake Analytics** obliczeniowe połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="389f7-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="389f7-117">Przed utworzeniem potoku z działaniem Data Lake Analytics U-SQL, należy utworzyć konto usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="389f7-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="389f7-118">toolearn dotyczące usługi Azure Data Lake Analytics, zobacz [Rozpoczynanie pracy z usługą Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="389f7-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="389f7-119">Przejrzyj hello [kompilacji pierwszy samouczek potoku](data-factory-build-your-first-pipeline.md) dla toocreate szczegółowy opis kroków fabryki danych, połączone usługi, zestawy danych i potoku.</span><span class="sxs-lookup"><span data-stu-id="389f7-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="389f7-120">Za pomocą fragmenty kodu JSON Edytor fabryki danych i jednostek fabryki danych toocreate programu Visual Studio lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="389f7-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="389f7-121">Typy obsługiwane uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="389f7-121">Supported authentication types</span></span>
<span data-ttu-id="389f7-122">Działanie U-SQL obsługuje poniżej typy uwierzytelniania względem usługi Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="389f7-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="389f7-123">Uwierzytelnianie jednostki usługi</span><span class="sxs-lookup"><span data-stu-id="389f7-123">Service principal authentication</span></span>
* <span data-ttu-id="389f7-124">Uwierzytelnianie użytkownika poświadczeń (OAuth)</span><span class="sxs-lookup"><span data-stu-id="389f7-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="389f7-125">Firma Microsoft zaleca korzystanie z uwierzytelniania głównej usługi, zwłaszcza w przypadku zaplanowane wykonanie U-SQL.</span><span class="sxs-lookup"><span data-stu-id="389f7-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="389f7-126">Zachowanie wygaśnięcia tokenu może wystąpić przy użyciu uwierzytelniania poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="389f7-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="389f7-127">Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#azure-data-lake-analytics-linked-service) sekcji.</span><span class="sxs-lookup"><span data-stu-id="389f7-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="389f7-128">Usługi Azure Data Lake Analytics połączona usługa</span><span class="sxs-lookup"><span data-stu-id="389f7-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="389f7-129">Możesz utworzyć **Azure Data Lake Analytics** połączone toolink usługi fabryki danych Azure tooan usługi Azure Data Lake Analytics obliczeń.</span><span class="sxs-lookup"><span data-stu-id="389f7-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="389f7-130">Data Lake Analytics U-SQL działania w potoku hello Hello odwołuje się toothis połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="389f7-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="389f7-131">Witaj Poniższa tabela zawiera opisy hello ogólne właściwości używane w hello definicji JSON.</span><span class="sxs-lookup"><span data-stu-id="389f7-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="389f7-132">Dodatkowo można wybrać nazwy głównej usługi i uwierzytelnianie poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="389f7-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="389f7-133">Właściwość</span><span class="sxs-lookup"><span data-stu-id="389f7-133">Property</span></span> | <span data-ttu-id="389f7-134">Opis</span><span class="sxs-lookup"><span data-stu-id="389f7-134">Description</span></span> | <span data-ttu-id="389f7-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="389f7-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="389f7-136">**Typ**</span><span class="sxs-lookup"><span data-stu-id="389f7-136">**type**</span></span> |<span data-ttu-id="389f7-137">powinien mieć ustawioną właściwość type Hello: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="389f7-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="389f7-138">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-138">Yes</span></span> |
| <span data-ttu-id="389f7-139">**Nazwa konta**</span><span class="sxs-lookup"><span data-stu-id="389f7-139">**accountName**</span></span> |<span data-ttu-id="389f7-140">Nazwa konta usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="389f7-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="389f7-141">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-141">Yes</span></span> |
| <span data-ttu-id="389f7-142">**Element dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="389f7-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="389f7-143">Identyfikator URI, usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="389f7-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="389f7-144">Nie</span><span class="sxs-lookup"><span data-stu-id="389f7-144">No</span></span> |
| <span data-ttu-id="389f7-145">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="389f7-145">**subscriptionId**</span></span> |<span data-ttu-id="389f7-146">Identyfikator subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="389f7-146">Azure subscription id</span></span> |<span data-ttu-id="389f7-147">Nie (Jeśli nie określono subskrypcji hello jest używana fabryka danych).</span><span class="sxs-lookup"><span data-stu-id="389f7-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="389f7-148">**grupy zasobów o nazwie**</span><span class="sxs-lookup"><span data-stu-id="389f7-148">**resourceGroupName**</span></span> |<span data-ttu-id="389f7-149">Nazwa grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="389f7-149">Azure resource group name</span></span> |<span data-ttu-id="389f7-150">Nie (Jeśli nie określono grupy zasobów hello jest używana fabryka danych).</span><span class="sxs-lookup"><span data-stu-id="389f7-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="389f7-151">Uwierzytelnianie główna usługi (zalecane)</span><span class="sxs-lookup"><span data-stu-id="389f7-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="389f7-152">główne uwierzytelnianie usługi toouse rejestru jednostki aplikacji w usłudze Azure Active Directory (Azure AD) i udziel go hello dostępu tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="389f7-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="389f7-153">Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="389f7-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="389f7-154">Zwróć uwagę na powitania następujące wartości, których używasz toodefine hello połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="389f7-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="389f7-155">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="389f7-155">Application ID</span></span>
* <span data-ttu-id="389f7-156">Klucz aplikacji</span><span class="sxs-lookup"><span data-stu-id="389f7-156">Application key</span></span> 
* <span data-ttu-id="389f7-157">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="389f7-157">Tenant ID</span></span>

<span data-ttu-id="389f7-158">Uwierzytelnianie usługi głównej określając hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="389f7-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="389f7-159">Właściwość</span><span class="sxs-lookup"><span data-stu-id="389f7-159">Property</span></span> | <span data-ttu-id="389f7-160">Opis</span><span class="sxs-lookup"><span data-stu-id="389f7-160">Description</span></span> | <span data-ttu-id="389f7-161">Wymagane</span><span class="sxs-lookup"><span data-stu-id="389f7-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="389f7-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="389f7-162">**servicePrincipalId**</span></span> | <span data-ttu-id="389f7-163">Określ identyfikator aplikacji hello klienta.</span><span class="sxs-lookup"><span data-stu-id="389f7-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="389f7-164">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-164">Yes</span></span> |
| <span data-ttu-id="389f7-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="389f7-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="389f7-166">Określ klucz aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-166">Specify hello application's key.</span></span> | <span data-ttu-id="389f7-167">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-167">Yes</span></span> |
| <span data-ttu-id="389f7-168">**dzierżawy**</span><span class="sxs-lookup"><span data-stu-id="389f7-168">**tenant**</span></span> | <span data-ttu-id="389f7-169">Określ informacje dzierżawy hello (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja.</span><span class="sxs-lookup"><span data-stu-id="389f7-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="389f7-170">Można go pobrać aktywowania hello myszy w prawym górnym narożniku hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="389f7-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="389f7-171">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-171">Yes</span></span> |

<span data-ttu-id="389f7-172">**Przykład: Usługa podmiotu zabezpieczeń uwierzytelniania**</span><span class="sxs-lookup"><span data-stu-id="389f7-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="389f7-173">Uwierzytelnianie poświadczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="389f7-173">User credential authentication</span></span>
<span data-ttu-id="389f7-174">Alternatywnie można uwierzytelnienia poświadczeń użytkownika dla usługi Data Lake Analytics, określając hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="389f7-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="389f7-175">Właściwość</span><span class="sxs-lookup"><span data-stu-id="389f7-175">Property</span></span> | <span data-ttu-id="389f7-176">Opis</span><span class="sxs-lookup"><span data-stu-id="389f7-176">Description</span></span> | <span data-ttu-id="389f7-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="389f7-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="389f7-178">**autoryzacji**</span><span class="sxs-lookup"><span data-stu-id="389f7-178">**authorization**</span></span> | <span data-ttu-id="389f7-179">Kliknij przycisk hello **autoryzacji** przycisku na powitania Edytor fabryki danych i wprowadź Twoje poświadczenia przypisującej właściwość toothis hello wygenerowana automatycznie autoryzacji URL.</span><span class="sxs-lookup"><span data-stu-id="389f7-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="389f7-180">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-180">Yes</span></span> |
| <span data-ttu-id="389f7-181">**Identyfikator sesji**</span><span class="sxs-lookup"><span data-stu-id="389f7-181">**sessionId**</span></span> | <span data-ttu-id="389f7-182">Identyfikator sesji OAuth z sesji autoryzacji OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="389f7-183">Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="389f7-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="389f7-184">To ustawienie jest automatycznie generowany, gdy używasz hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="389f7-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="389f7-185">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-185">Yes</span></span> |

<span data-ttu-id="389f7-186">**Przykład: Użytkownik poświadczeń uwierzytelniania**</span><span class="sxs-lookup"><span data-stu-id="389f7-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="389f7-187">Wygaśnięcia tokenu</span><span class="sxs-lookup"><span data-stu-id="389f7-187">Token expiration</span></span>
<span data-ttu-id="389f7-188">Witaj kod autoryzacji wygenerowanych przy użyciu hello **autoryzacji** przycisk wygaśnie po upływie pewnego czasu.</span><span class="sxs-lookup"><span data-stu-id="389f7-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="389f7-189">Zobacz hello na powitania czas wygaśnięcia dla różnych typów kont użytkowników w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="389f7-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="389f7-190">Może zostać wyświetlony następujący komunikat o błędzie hello hello podczas uwierzytelniania **wygaśnięcia tokenu**: poświadczeń błąd operacji: invalid_grant - AADSTS70002: błąd podczas sprawdzania poprawności poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="389f7-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="389f7-191">AADSTS70008: hello podać Udziel dostępu jest wygasnąć lub zostać odwołane.</span><span class="sxs-lookup"><span data-stu-id="389f7-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="389f7-192">Identyfikator śledzenia: Identyfikator korelacji d18629e8-af88-43c5-88e3-d8419eb1fca1: sygnatura czasowa fac30a0c-6be6-4e02-8d69-a776d2ffefd7: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="389f7-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="389f7-193">Typ użytkownika</span><span class="sxs-lookup"><span data-stu-id="389f7-193">User type</span></span> | <span data-ttu-id="389f7-194">Wygasa po</span><span class="sxs-lookup"><span data-stu-id="389f7-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="389f7-195">Konta użytkowników, które nie są zarządzane przez usługę Azure Active Directory (@hotmail.com, @live.comitp.)</span><span class="sxs-lookup"><span data-stu-id="389f7-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="389f7-196">12 godzin</span><span class="sxs-lookup"><span data-stu-id="389f7-196">12 hours</span></span> |
| <span data-ttu-id="389f7-197">Konta użytkowników zarządzanych przez usługi Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="389f7-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="389f7-198">Uruchom 14 dni od ostatniego wycinek hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="389f7-199">90 dni, jeśli wycinek oparte na podstawie OAuth połączonej usługi jest uruchamiana co najmniej raz na 14 dni.</span><span class="sxs-lookup"><span data-stu-id="389f7-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="389f7-200">tooavoid/Rozwiąż ten błąd, ponownie autoryzować przy użyciu hello **autoryzacji** przycisku hello **wygaśnięcia tokenu** i wdrożenie usługi hello połączone.</span><span class="sxs-lookup"><span data-stu-id="389f7-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="389f7-201">Można również tworzyć wartości **sessionId** i **autoryzacji** właściwości programowo przy użyciu kodu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="389f7-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="389f7-202">Zobacz [klasy AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [klasy AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), i [klasy AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tematy, aby uzyskać więcej informacji informacje o klasach fabryki danych hello używane w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="389f7-203">Dodaj odwołanie do: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll dla hello WindowsFormsWebAuthenticationDialog klasy.</span><span class="sxs-lookup"><span data-stu-id="389f7-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="389f7-204">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="389f7-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="389f7-205">powitania po fragment kodu JSON definiuje potoku z działaniem Data Lake Analytics U-SQL.</span><span class="sxs-lookup"><span data-stu-id="389f7-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="389f7-206">Definicja działania Hello ma toohello odwołanie do usługi Azure Data Lake Analytics połączone, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="389f7-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="389f7-207">Witaj poniższej tabeli opisano nazwy i opisy właściwości, które są określone toothis działania.</span><span class="sxs-lookup"><span data-stu-id="389f7-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="389f7-208">Właściwość</span><span class="sxs-lookup"><span data-stu-id="389f7-208">Property</span></span> | <span data-ttu-id="389f7-209">Opis</span><span class="sxs-lookup"><span data-stu-id="389f7-209">Description</span></span> | <span data-ttu-id="389f7-210">Wymagane</span><span class="sxs-lookup"><span data-stu-id="389f7-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="389f7-211">type</span><span class="sxs-lookup"><span data-stu-id="389f7-211">type</span></span> |<span data-ttu-id="389f7-212">zbyt należy ustawić właściwość typu Hello**DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="389f7-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="389f7-213">Tak</span><span class="sxs-lookup"><span data-stu-id="389f7-213">Yes</span></span> |
| <span data-ttu-id="389f7-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="389f7-214">scriptPath</span></span> |<span data-ttu-id="389f7-215">Ścieżka toofolder, zawierający skrypt hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="389f7-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="389f7-216">Nazwa pliku hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="389f7-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="389f7-217">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="389f7-217">No (if you use script)</span></span> |
| <span data-ttu-id="389f7-218">Element scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="389f7-218">scriptLinkedService</span></span> |<span data-ttu-id="389f7-219">Połączonej usługi, która łączy hello magazynu, który zawiera hello skryptu toohello usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="389f7-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="389f7-220">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="389f7-220">No (if you use script)</span></span> |
| <span data-ttu-id="389f7-221">Skrypt</span><span class="sxs-lookup"><span data-stu-id="389f7-221">script</span></span> |<span data-ttu-id="389f7-222">Określ skrypt wbudowany zamiast określania scriptPath i scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="389f7-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="389f7-223">Na przykład: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="389f7-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="389f7-224">Nie (Jeśli używasz scriptPath i scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="389f7-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="389f7-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="389f7-225">degreeOfParallelism</span></span> |<span data-ttu-id="389f7-226">Maksymalna liczba węzłów Hello używać jednocześnie toorun hello zadania.</span><span class="sxs-lookup"><span data-stu-id="389f7-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="389f7-227">Nie</span><span class="sxs-lookup"><span data-stu-id="389f7-227">No</span></span> |
| <span data-ttu-id="389f7-228">Priorytet</span><span class="sxs-lookup"><span data-stu-id="389f7-228">priority</span></span> |<span data-ttu-id="389f7-229">Określa, które spośród wszystkich znajdujących się w kolejce zadań powinna być wybranego toorun najpierw.</span><span class="sxs-lookup"><span data-stu-id="389f7-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="389f7-230">Witaj hello niższą, wyższy priorytet hello hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="389f7-231">Nie</span><span class="sxs-lookup"><span data-stu-id="389f7-231">No</span></span> |
| <span data-ttu-id="389f7-232">parameters</span><span class="sxs-lookup"><span data-stu-id="389f7-232">parameters</span></span> |<span data-ttu-id="389f7-233">Parametry skryptu hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="389f7-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="389f7-234">Nie</span><span class="sxs-lookup"><span data-stu-id="389f7-234">No</span></span> |
| <span data-ttu-id="389f7-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="389f7-235">runtimeVersion</span></span> | <span data-ttu-id="389f7-236">Wersja środowiska uruchomieniowego toouse aparat hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="389f7-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="389f7-237">Nie</span><span class="sxs-lookup"><span data-stu-id="389f7-237">No</span></span> | 
| <span data-ttu-id="389f7-238">właściwość compilationMode</span><span class="sxs-lookup"><span data-stu-id="389f7-238">compilationMode</span></span> | <p><span data-ttu-id="389f7-239">Tryb kompilacji U-SQL.</span><span class="sxs-lookup"><span data-stu-id="389f7-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="389f7-240">Musi być jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="389f7-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="389f7-241">**Semantycznej:** wykonywać tylko semantycznego kontroli i potrzeby związane z poprawnością kontroli.</span><span class="sxs-lookup"><span data-stu-id="389f7-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="389f7-242">**Pełna:** wykonania pełnej kompilacji hello, w tym sprawdzanie składni, optymalizacja, generowanie kodu itp.</span><span class="sxs-lookup"><span data-stu-id="389f7-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="389f7-243">**SingleBox:** wykonania pełnej kompilacji hello z tooSingleBox ustawienie TargetType.</span><span class="sxs-lookup"><span data-stu-id="389f7-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="389f7-244">Jeśli nie określisz wartości dla tej właściwości, powitania serwera określa tryb kompilacji optymalne hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="389f7-245">Nie</span><span class="sxs-lookup"><span data-stu-id="389f7-245">No</span></span> | 

<span data-ttu-id="389f7-246">Zobacz [definicji skryptu SearchLogProcessing.txt](#sample-u-sql-script) hello definicji skryptu.</span><span class="sxs-lookup"><span data-stu-id="389f7-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="389f7-247">Przykładowe dane wejściowe i wyjściowe zestawy danych</span><span class="sxs-lookup"><span data-stu-id="389f7-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="389f7-248">Wejściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="389f7-248">Input dataset</span></span>
<span data-ttu-id="389f7-249">W tym przykładzie danych wejściowych hello znajduje się w usłudze Azure Data Lake Store (plik SearchLog.tsv plik w folderze datalake/wprowadzania hello).</span><span class="sxs-lookup"><span data-stu-id="389f7-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
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
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="389f7-250">Wyjściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="389f7-250">Output dataset</span></span>
<span data-ttu-id="389f7-251">W tym przykładzie danych wyjściowych hello utworzonego przez hello skryptu U-SQL jest przechowywane w Azure Data Lake Store (datalake/wyjścia folder).</span><span class="sxs-lookup"><span data-stu-id="389f7-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="389f7-252">Przykładowe Data Lake Store połączona usługa</span><span class="sxs-lookup"><span data-stu-id="389f7-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="389f7-253">Oto definicji hello próbki hello Azure Data Lake Store połączonej usługi używana przez zestaw danych hello wejścia/wyjścia.</span><span class="sxs-lookup"><span data-stu-id="389f7-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="389f7-254">Zobacz [przenieść tooand danych z usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md) artykułu Opis właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="389f7-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="389f7-255">Przykładowy skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="389f7-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="389f7-256">Witaj wartości  **@in**  i  **@out**  Parametry skryptu U-SQL hello są przekazywane dynamicznie przez ADF z sekcją "parameters" hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="389f7-257">Zobacz sekcję "parameters" hello w definicji potoku hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="389f7-258">Inne właściwości, takie jak degreeOfParallelism i priorytet można określić również w definicji potoku prac hello działające na powitania usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="389f7-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="389f7-259">Parametry dynamiczne</span><span class="sxs-lookup"><span data-stu-id="389f7-259">Dynamic parameters</span></span>
<span data-ttu-id="389f7-260">W definicji potoku próbki hello i wylogowywanie parametry są przypisywane z zakodowanych wartości.</span><span class="sxs-lookup"><span data-stu-id="389f7-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="389f7-261">Zamiast niego jest możliwe toouse parametrów dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="389f7-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="389f7-262">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="389f7-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="389f7-263">W takim przypadku pliki wejściowe nadal są pobierane z folderu /datalake/input hello i pliki wyjściowe są generowane w folderze /datalake/output hello.</span><span class="sxs-lookup"><span data-stu-id="389f7-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="389f7-264">nazwy plików Hello są dynamiczne na podstawie czasu rozpoczęcia hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="389f7-264">hello file names are dynamic based on hello slice start time.</span></span>  

