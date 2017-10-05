---
title: "Przekształcanie danych za pomocą skryptu U-SQL - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się sposobu przetwarzania lub Przekształcanie danych za pomocą skryptów U-SQL w usłudze obliczeniowych Azure Data Lake Analytics."
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
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="03c43-103">Przekształcanie danych za pomocą skryptów U-SQL w usłudze Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="03c43-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="03c43-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="03c43-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="03c43-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="03c43-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="03c43-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="03c43-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="03c43-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="03c43-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="03c43-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="03c43-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="03c43-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="03c43-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="03c43-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="03c43-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="03c43-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="03c43-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="03c43-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="03c43-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="03c43-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="03c43-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="03c43-114">Potok w fabryce danych Azure przetwarza dane w usługach magazynu połączone, przy użyciu obliczeniowego połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="03c43-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="03c43-115">Zawiera sekwencję działań, gdzie każde działanie wykonuje operację przetwarzania specyficznego dla.</span><span class="sxs-lookup"><span data-stu-id="03c43-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="03c43-116">W tym artykule opisano **Data Lake Analytics U-SQL działania** , na którym działa **U-SQL** skryptom na **Azure Data Lake Analytics** obliczeniowe połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="03c43-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="03c43-117">Przed utworzeniem potoku z działaniem Data Lake Analytics U-SQL, należy utworzyć konto usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="03c43-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="03c43-118">Aby zapoznać się z usługą Azure Data Lake Analytics, zobacz [Rozpoczynanie pracy z usługą Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03c43-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="03c43-119">Przegląd [kompilacji pierwszy samouczek potoku](data-factory-build-your-first-pipeline.md) szczegółowy opis kroków można utworzyć fabryki danych, połączone usługi, zestawy danych i potoku.</span><span class="sxs-lookup"><span data-stu-id="03c43-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="03c43-120">Za pomocą fragmenty kodu JSON Edytor fabryki danych lub Visual Studio lub Azure PowerShell do tworzenia jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="03c43-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="03c43-121">Typy obsługiwane uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="03c43-121">Supported authentication types</span></span>
<span data-ttu-id="03c43-122">Działanie U-SQL obsługuje poniżej typy uwierzytelniania względem usługi Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="03c43-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="03c43-123">Uwierzytelnianie jednostki usługi</span><span class="sxs-lookup"><span data-stu-id="03c43-123">Service principal authentication</span></span>
* <span data-ttu-id="03c43-124">Uwierzytelnianie użytkownika poświadczeń (OAuth)</span><span class="sxs-lookup"><span data-stu-id="03c43-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="03c43-125">Firma Microsoft zaleca korzystanie z uwierzytelniania głównej usługi, zwłaszcza w przypadku zaplanowane wykonanie U-SQL.</span><span class="sxs-lookup"><span data-stu-id="03c43-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="03c43-126">Zachowanie wygaśnięcia tokenu może wystąpić przy użyciu uwierzytelniania poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03c43-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="03c43-127">Szczegółowe informacje dotyczące konfiguracji, zobacz [połączona usługa właściwości](#azure-data-lake-analytics-linked-service) sekcji.</span><span class="sxs-lookup"><span data-stu-id="03c43-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="03c43-128">Usługi Azure Data Lake Analytics połączona usługa</span><span class="sxs-lookup"><span data-stu-id="03c43-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="03c43-129">Możesz utworzyć **Azure Data Lake Analytics** połączonej usługi, aby połączyć z usługą Azure Data Lake Analytics obliczeniowe usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="03c43-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="03c43-130">Data Lake Analytics U-SQL działania w potoku odwołuje się do tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="03c43-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="03c43-131">Poniższa tabela zawiera opisy ogólne właściwości używane w definicji JSON.</span><span class="sxs-lookup"><span data-stu-id="03c43-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="03c43-132">Dodatkowo można wybrać nazwy głównej usługi i uwierzytelnianie poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03c43-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="03c43-133">Właściwość</span><span class="sxs-lookup"><span data-stu-id="03c43-133">Property</span></span> | <span data-ttu-id="03c43-134">Opis</span><span class="sxs-lookup"><span data-stu-id="03c43-134">Description</span></span> | <span data-ttu-id="03c43-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="03c43-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03c43-136">**Typ**</span><span class="sxs-lookup"><span data-stu-id="03c43-136">**type**</span></span> |<span data-ttu-id="03c43-137">Powinien mieć ustawioną właściwość type: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="03c43-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="03c43-138">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-138">Yes</span></span> |
| <span data-ttu-id="03c43-139">**Nazwa konta**</span><span class="sxs-lookup"><span data-stu-id="03c43-139">**accountName**</span></span> |<span data-ttu-id="03c43-140">Nazwa konta usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="03c43-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="03c43-141">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-141">Yes</span></span> |
| <span data-ttu-id="03c43-142">**Element dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="03c43-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="03c43-143">Identyfikator URI, usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="03c43-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="03c43-144">Nie</span><span class="sxs-lookup"><span data-stu-id="03c43-144">No</span></span> |
| <span data-ttu-id="03c43-145">**Identyfikator subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="03c43-145">**subscriptionId**</span></span> |<span data-ttu-id="03c43-146">Identyfikator subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="03c43-146">Azure subscription id</span></span> |<span data-ttu-id="03c43-147">Nie (Jeśli nie zostanie określony, używany subskrypcji fabryki danych).</span><span class="sxs-lookup"><span data-stu-id="03c43-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="03c43-148">**grupy zasobów o nazwie**</span><span class="sxs-lookup"><span data-stu-id="03c43-148">**resourceGroupName**</span></span> |<span data-ttu-id="03c43-149">Nazwa grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="03c43-149">Azure resource group name</span></span> |<span data-ttu-id="03c43-150">Nie (Jeśli nie zostanie określony, używana grupa zasobów z fabryką danych).</span><span class="sxs-lookup"><span data-stu-id="03c43-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="03c43-151">Uwierzytelnianie główna usługi (zalecane)</span><span class="sxs-lookup"><span data-stu-id="03c43-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="03c43-152">Aby używać uwierzytelniania głównej usługi, Zarejestruj podmiot aplikacji w usłudze Azure Active Directory (Azure AD) i przyznać jej dostęp do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="03c43-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="03c43-153">Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="03c43-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="03c43-154">Zwróć uwagę na następujące wartości, które służą do definiowania połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="03c43-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="03c43-155">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="03c43-155">Application ID</span></span>
* <span data-ttu-id="03c43-156">Klucz aplikacji</span><span class="sxs-lookup"><span data-stu-id="03c43-156">Application key</span></span> 
* <span data-ttu-id="03c43-157">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="03c43-157">Tenant ID</span></span>

<span data-ttu-id="03c43-158">Uwierzytelnianie usługi głównej przez określenie następujących właściwości:</span><span class="sxs-lookup"><span data-stu-id="03c43-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="03c43-159">Właściwość</span><span class="sxs-lookup"><span data-stu-id="03c43-159">Property</span></span> | <span data-ttu-id="03c43-160">Opis</span><span class="sxs-lookup"><span data-stu-id="03c43-160">Description</span></span> | <span data-ttu-id="03c43-161">Wymagane</span><span class="sxs-lookup"><span data-stu-id="03c43-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="03c43-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="03c43-162">**servicePrincipalId**</span></span> | <span data-ttu-id="03c43-163">Określ identyfikator aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="03c43-163">Specify the application's client ID.</span></span> | <span data-ttu-id="03c43-164">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-164">Yes</span></span> |
| <span data-ttu-id="03c43-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="03c43-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="03c43-166">Określ klucz aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03c43-166">Specify the application's key.</span></span> | <span data-ttu-id="03c43-167">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-167">Yes</span></span> |
| <span data-ttu-id="03c43-168">**dzierżawy**</span><span class="sxs-lookup"><span data-stu-id="03c43-168">**tenant**</span></span> | <span data-ttu-id="03c43-169">Określ informacje dzierżawy (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja.</span><span class="sxs-lookup"><span data-stu-id="03c43-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="03c43-170">Można go pobrać, ustawiając kursor myszy w prawym górnym rogu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="03c43-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="03c43-171">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-171">Yes</span></span> |

<span data-ttu-id="03c43-172">**Przykład: Usługa podmiotu zabezpieczeń uwierzytelniania**</span><span class="sxs-lookup"><span data-stu-id="03c43-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="03c43-173">Uwierzytelnianie poświadczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="03c43-173">User credential authentication</span></span>
<span data-ttu-id="03c43-174">Alternatywnie można uwierzytelnienia poświadczeń użytkownika dla usługi Data Lake Analytics przez określenie następujących właściwości:</span><span class="sxs-lookup"><span data-stu-id="03c43-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="03c43-175">Właściwość</span><span class="sxs-lookup"><span data-stu-id="03c43-175">Property</span></span> | <span data-ttu-id="03c43-176">Opis</span><span class="sxs-lookup"><span data-stu-id="03c43-176">Description</span></span> | <span data-ttu-id="03c43-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="03c43-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="03c43-178">**autoryzacji**</span><span class="sxs-lookup"><span data-stu-id="03c43-178">**authorization**</span></span> | <span data-ttu-id="03c43-179">Kliknij przycisk **autoryzacji** przycisk Edytor fabryki danych i wprowadź Twoje poświadczenia, który przypisuje do tej właściwości adresu URL autoryzacji wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="03c43-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="03c43-180">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-180">Yes</span></span> |
| <span data-ttu-id="03c43-181">**Identyfikator sesji**</span><span class="sxs-lookup"><span data-stu-id="03c43-181">**sessionId**</span></span> | <span data-ttu-id="03c43-182">Identyfikator sesji OAuth z sesji autoryzacji OAuth.</span><span class="sxs-lookup"><span data-stu-id="03c43-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="03c43-183">Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="03c43-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="03c43-184">To ustawienie jest generowane automatycznie, gdy używasz Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="03c43-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="03c43-185">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-185">Yes</span></span> |

<span data-ttu-id="03c43-186">**Przykład: Użytkownik poświadczeń uwierzytelniania**</span><span class="sxs-lookup"><span data-stu-id="03c43-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="03c43-187">Wygaśnięcia tokenu</span><span class="sxs-lookup"><span data-stu-id="03c43-187">Token expiration</span></span>
<span data-ttu-id="03c43-188">Kod autoryzacji wygenerowanych przy użyciu **autoryzacji** przycisk wygaśnie po upływie pewnego czasu.</span><span class="sxs-lookup"><span data-stu-id="03c43-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="03c43-189">Czas wygaśnięcia dla różnych typów kont użytkowników znajduje się w tabeli poniżej.</span><span class="sxs-lookup"><span data-stu-id="03c43-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="03c43-190">Może zostać wyświetlony następujący błąd komunikatu podczas uwierzytelniania **wygaśnięcia tokenu**: poświadczeń błąd operacji: invalid_grant - AADSTS70002: błąd podczas sprawdzania poprawności poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="03c43-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="03c43-191">AADSTS70008: Udzielone prawa dostępu jest wygasnąć lub zostać odwołane.</span><span class="sxs-lookup"><span data-stu-id="03c43-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="03c43-192">Identyfikator śledzenia: Identyfikator korelacji d18629e8-af88-43c5-88e3-d8419eb1fca1: sygnatura czasowa fac30a0c-6be6-4e02-8d69-a776d2ffefd7: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="03c43-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="03c43-193">Typ użytkownika</span><span class="sxs-lookup"><span data-stu-id="03c43-193">User type</span></span> | <span data-ttu-id="03c43-194">Wygasa po</span><span class="sxs-lookup"><span data-stu-id="03c43-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="03c43-195">Konta użytkowników, które nie są zarządzane przez usługę Azure Active Directory (@hotmail.com, @live.comitp.)</span><span class="sxs-lookup"><span data-stu-id="03c43-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="03c43-196">12 godzin</span><span class="sxs-lookup"><span data-stu-id="03c43-196">12 hours</span></span> |
| <span data-ttu-id="03c43-197">Konta użytkowników zarządzanych przez usługi Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="03c43-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="03c43-198">Uruchom 14 dni od ostatniego wycinka.</span><span class="sxs-lookup"><span data-stu-id="03c43-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="03c43-199">90 dni, jeśli wycinek oparte na podstawie OAuth połączonej usługi jest uruchamiana co najmniej raz na 14 dni.</span><span class="sxs-lookup"><span data-stu-id="03c43-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="03c43-200">Aby uniknąć/Rozwiąż ten błąd, ponownie autoryzować przy użyciu **autoryzacji** przycisku, gdy **wygaśnięcia tokenu** i wdrożenie połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="03c43-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="03c43-201">Można również tworzyć wartości **sessionId** i **autoryzacji** właściwości programowo przy użyciu kodu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="03c43-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="03c43-202">Zobacz [klasy AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [klasy AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), i [klasy AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tematy, aby uzyskać więcej informacji o klasach fabryki danych używana w kodzie.</span><span class="sxs-lookup"><span data-stu-id="03c43-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="03c43-203">Dodaj odwołanie do: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll dla klasy WindowsFormsWebAuthenticationDialog.</span><span class="sxs-lookup"><span data-stu-id="03c43-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="03c43-204">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="03c43-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="03c43-205">Poniższy fragment kodu JSON definiuje potoku z działaniem Data Lake Analytics U-SQL.</span><span class="sxs-lookup"><span data-stu-id="03c43-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="03c43-206">Definicji działania zawiera odwołanie do usługi Azure Data Lake Analytics połączone utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="03c43-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="03c43-207">W poniższej tabeli opisano nazwy i opisy właściwości, które są specyficzne dla tego działania.</span><span class="sxs-lookup"><span data-stu-id="03c43-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="03c43-208">Właściwość</span><span class="sxs-lookup"><span data-stu-id="03c43-208">Property</span></span> | <span data-ttu-id="03c43-209">Opis</span><span class="sxs-lookup"><span data-stu-id="03c43-209">Description</span></span> | <span data-ttu-id="03c43-210">Wymagane</span><span class="sxs-lookup"><span data-stu-id="03c43-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="03c43-211">type</span><span class="sxs-lookup"><span data-stu-id="03c43-211">type</span></span> |<span data-ttu-id="03c43-212">Właściwość type musi mieć ustawioną **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="03c43-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="03c43-213">Tak</span><span class="sxs-lookup"><span data-stu-id="03c43-213">Yes</span></span> |
| <span data-ttu-id="03c43-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="03c43-214">scriptPath</span></span> |<span data-ttu-id="03c43-215">Ścieżka do folderu, który zawiera skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="03c43-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="03c43-216">Nazwa pliku jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="03c43-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="03c43-217">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="03c43-217">No (if you use script)</span></span> |
| <span data-ttu-id="03c43-218">Element scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="03c43-218">scriptLinkedService</span></span> |<span data-ttu-id="03c43-219">Połączonej usługi, która łączy magazynu, który zawiera skrypt do fabryki danych</span><span class="sxs-lookup"><span data-stu-id="03c43-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="03c43-220">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="03c43-220">No (if you use script)</span></span> |
| <span data-ttu-id="03c43-221">Skrypt</span><span class="sxs-lookup"><span data-stu-id="03c43-221">script</span></span> |<span data-ttu-id="03c43-222">Określ skrypt wbudowany zamiast określania scriptPath i scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="03c43-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="03c43-223">Na przykład: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="03c43-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="03c43-224">Nie (Jeśli używasz scriptPath i scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="03c43-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="03c43-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="03c43-225">degreeOfParallelism</span></span> |<span data-ttu-id="03c43-226">Maksymalna liczba węzłów jednocześnie użyta do uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="03c43-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="03c43-227">Nie</span><span class="sxs-lookup"><span data-stu-id="03c43-227">No</span></span> |
| <span data-ttu-id="03c43-228">Priorytet</span><span class="sxs-lookup"><span data-stu-id="03c43-228">priority</span></span> |<span data-ttu-id="03c43-229">Określa, które spośród wszystkich znajdujących się w kolejce zadań należy wybrać ma być uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="03c43-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="03c43-230">Im niższy numer, tym wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="03c43-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="03c43-231">Nie</span><span class="sxs-lookup"><span data-stu-id="03c43-231">No</span></span> |
| <span data-ttu-id="03c43-232">Parametry</span><span class="sxs-lookup"><span data-stu-id="03c43-232">parameters</span></span> |<span data-ttu-id="03c43-233">Parametry skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="03c43-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="03c43-234">Nie</span><span class="sxs-lookup"><span data-stu-id="03c43-234">No</span></span> |
| <span data-ttu-id="03c43-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="03c43-235">runtimeVersion</span></span> | <span data-ttu-id="03c43-236">Wersja środowiska uruchomieniowego aparatu U-SQL do użycia</span><span class="sxs-lookup"><span data-stu-id="03c43-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="03c43-237">Nie</span><span class="sxs-lookup"><span data-stu-id="03c43-237">No</span></span> | 
| <span data-ttu-id="03c43-238">właściwość compilationMode</span><span class="sxs-lookup"><span data-stu-id="03c43-238">compilationMode</span></span> | <p><span data-ttu-id="03c43-239">Tryb kompilacji U-SQL.</span><span class="sxs-lookup"><span data-stu-id="03c43-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="03c43-240">Musi być jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="03c43-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="03c43-241">**Semantycznej:** wykonywać tylko semantycznego kontroli i potrzeby związane z poprawnością kontroli.</span><span class="sxs-lookup"><span data-stu-id="03c43-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="03c43-242">**Pełna:** wykonania pełnej kompilacji, takich jak sprawdzanie składni, optymalizacja, generowania kodu, itp.</span><span class="sxs-lookup"><span data-stu-id="03c43-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="03c43-243">**SingleBox:** wykonania pełnej kompilacji, z ustawieniem TargetType do SingleBox.</span><span class="sxs-lookup"><span data-stu-id="03c43-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="03c43-244">Jeśli nie określisz wartości dla tej właściwości, serwer określa tryb optymalne kompilacji.</span><span class="sxs-lookup"><span data-stu-id="03c43-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="03c43-245">Nie</span><span class="sxs-lookup"><span data-stu-id="03c43-245">No</span></span> | 

<span data-ttu-id="03c43-246">Zobacz [definicji skryptu SearchLogProcessing.txt](#sample-u-sql-script) definicji skryptu.</span><span class="sxs-lookup"><span data-stu-id="03c43-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="03c43-247">Przykładowe dane wejściowe i wyjściowe zestawy danych</span><span class="sxs-lookup"><span data-stu-id="03c43-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="03c43-248">Wejściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="03c43-248">Input dataset</span></span>
<span data-ttu-id="03c43-249">W tym przykładzie dane wejściowe znajduje się w usłudze Azure Data Lake Store (plik SearchLog.tsv plik w folderze datalake/wprowadzania).</span><span class="sxs-lookup"><span data-stu-id="03c43-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="03c43-250">Wyjściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="03c43-250">Output dataset</span></span>
<span data-ttu-id="03c43-251">W tym przykładzie danych wyjściowych generowanych przez skrypt U-SQL jest przechowywane w usłudze Azure Data Lake Store (datalake/wyjścia folder).</span><span class="sxs-lookup"><span data-stu-id="03c43-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="03c43-252">Przykładowe Data Lake Store połączona usługa</span><span class="sxs-lookup"><span data-stu-id="03c43-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="03c43-253">W tym miejscu znajduje się definicja próbki Azure Data Lake Store połączonej usługi używana przez zestaw danych wejścia/wyjścia.</span><span class="sxs-lookup"><span data-stu-id="03c43-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

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

<span data-ttu-id="03c43-254">Zobacz [przenoszenie danych do i z usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md) artykułu Opis właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="03c43-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="03c43-255">Przykładowy skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="03c43-255">Sample U-SQL Script</span></span>

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
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="03c43-256">Wartości  **@in**  i  **@out**  Parametry skryptu U-SQL są przekazywane dynamicznie przez ADF zgodnie z sekcją "parameters".</span><span class="sxs-lookup"><span data-stu-id="03c43-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="03c43-257">Zobacz sekcję "parameters" w definicji potoku.</span><span class="sxs-lookup"><span data-stu-id="03c43-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="03c43-258">Inne właściwości, takie jak degreeOfParallelism i priorytet można określić również w definicji potoku dla zadań, które są uruchamiane w usłudze Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="03c43-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="03c43-259">Parametry dynamiczne</span><span class="sxs-lookup"><span data-stu-id="03c43-259">Dynamic parameters</span></span>
<span data-ttu-id="03c43-260">W definicji potoku próbki i wylogowywanie parametry są przypisywane z zakodowanych wartości.</span><span class="sxs-lookup"><span data-stu-id="03c43-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="03c43-261">Istnieje możliwość zamiast tego użyj parametrów dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="03c43-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="03c43-262">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="03c43-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="03c43-263">W takim przypadku pliki wejściowe nadal są pobierane z folderu /datalake/input i pliki wyjściowe są generowane w folderze /datalake/output.</span><span class="sxs-lookup"><span data-stu-id="03c43-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="03c43-264">Nazwy plików są dynamiczne na podstawie czasu rozpoczęcia wycinka.</span><span class="sxs-lookup"><span data-stu-id="03c43-264">The file names are dynamic based on the slice start time.</span></span>  

