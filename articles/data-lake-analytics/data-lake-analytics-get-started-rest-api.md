---
title: "Rozpoczynanie pracy z usługą Data Lake Analytics z użyciem interfejsu API REST | Microsoft Docs"
description: "Korzystanie z interfejsów API REST WebHDFS w celu wykonywania operacji w usłudze Data Lake Analytics"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="baca3-103">Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="baca3-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="baca3-104">Dowiedz się, w jaki sposób można korzystać z interfejsów API REST WebHDFS oraz interfejsów API REST usługi Data Lake Analytics do zarządzania kontami, zadaniami i katalogiem usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="baca3-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="baca3-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="baca3-105">Prerequisites</span></span>
* <span data-ttu-id="baca3-106">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="baca3-106">**An Azure subscription**.</span></span> <span data-ttu-id="baca3-107">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="baca3-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="baca3-108">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baca3-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="baca3-109">Za pomocą aplikacji usługi Azure AD można uwierzytelnić aplikację usługi Data Lake Analytics w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="baca3-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="baca3-110">Istnieją różne metody uwierzytelniania w usłudze Azure AD: **uwierzytelnianie użytkowników końcowych** i **uwierzytelnianie między usługami**.</span><span class="sxs-lookup"><span data-stu-id="baca3-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="baca3-111">Instrukcje i dodatkowe informacje na temat uwierzytelniania można znaleźć w artykule [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) (Uwierzytelnianie w usłudze Data Lake Analytics przy użyciu usługi Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="baca3-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="baca3-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="baca3-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="baca3-113">W tym artykule wykorzystywane jest narzędzie cURL w celu zademonstrowania sposobu wykonywania wywołań interfejsu API REST względem konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="baca3-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="baca3-114">Uwierzytelnianie za pomocą usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="baca3-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="baca3-115">Istnieją dwie metody uwierzytelniania za pomocą usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baca3-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="baca3-116">Uwierzytelnianie użytkowników końcowych (interakcyjne)</span><span class="sxs-lookup"><span data-stu-id="baca3-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="baca3-117">W tej metodzie aplikacja wyświetla monit o zalogowanie się, po czym wszystkie operacje są wykonywane w kontekście zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="baca3-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="baca3-118">Wykonaj następujące kroki, aby przeprowadzić uwierzytelnianie interakcyjne:</span><span class="sxs-lookup"><span data-stu-id="baca3-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="baca3-119">Za pomocą aplikacji przekieruj użytkownika pod następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="baca3-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="baca3-120">Identyfikator \<REDIRECT-URI> musi być zakodowany na potrzeby adresu URL.</span><span class="sxs-lookup"><span data-stu-id="baca3-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="baca3-121">Dlatego w celu zapisania adresu https://localhost użyj ciągu `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="baca3-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="baca3-122">Na potrzeby tego samouczka możesz zastąpić symbole zastępcze w powyższym adresie URL i wkleić go w pasku adresu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="baca3-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="baca3-123">Nastąpi przekierowanie w celu uwierzytelniania przy użyciu identyfikatora logowania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="baca3-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="baca3-124">Gdy pomyślnie się zalogujesz, odpowiedź zostanie wyświetlona na pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="baca3-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="baca3-125">Odpowiedź będzie miała następujący format:</span><span class="sxs-lookup"><span data-stu-id="baca3-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="baca3-126">Przechwyć kod autoryzacji z odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="baca3-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="baca3-127">W ramach niniejszego samouczka możesz skopiować kod autoryzacji z paska adresu przeglądarki sieci web i przekazać go w żądaniu POST do punktu końcowego tokenu w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="baca3-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="baca3-128">W takim przypadku identyfikatora \<REDIRECT-URI> nie trzeba kodować.</span><span class="sxs-lookup"><span data-stu-id="baca3-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="baca3-129">Odpowiedzią jest obiekt JSON, który zawiera token dostępu (np. `"access_token": "<ACCESS_TOKEN>"`) oraz token odświeżania (np. `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="baca3-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="baca3-130">Aplikacja używa tokenu dostępu podczas uzyskiwania dostępu do usługi Azure Data Lake Store i tokenu odświeżania, aby uzyskać inny token dostępu w przypadku wygaśnięcia tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="baca3-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="baca3-131">Po wygaśnięciu tokenu dostępu możesz zażądać nowego tokenu dostępu, używając tokenu odświeżania w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="baca3-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="baca3-132">Więcej informacji na temat interakcyjnego uwierzytelniania użytkownika zawiera temat [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx) (Przepływ udzielania kodu autoryzacji).</span><span class="sxs-lookup"><span data-stu-id="baca3-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="baca3-133">Uwierzytelnianie między usługami (nieinterakcyjne)</span><span class="sxs-lookup"><span data-stu-id="baca3-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="baca3-134">Przy użyciu tej metody aplikacja udostępnia własne poświadczenia, aby wykonywać operacje.</span><span class="sxs-lookup"><span data-stu-id="baca3-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="baca3-135">W tym celu należy wygenerować żądanie POST, tak jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="baca3-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="baca3-136">Dane wyjściowe tego żądania będą zawierać token autoryzacji (oznaczony jako `access-token` w danych wyjściowych poniżej), który następnie będzie przekazywany w wywołaniach interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="baca3-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="baca3-137">Zapisz ten token uwierzytelniania w pliku tekstowym. Będzie on potrzebny w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="baca3-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="baca3-138">W tym artykule wykorzystano podejście **nieinterakcyjne**.</span><span class="sxs-lookup"><span data-stu-id="baca3-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="baca3-139">Więcej informacji na temat podejścia nieinterakcyjnego (wywołań między usługami) zawiera temat [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx) (Wywołania między usługami przy użyciu poświadczeń).</span><span class="sxs-lookup"><span data-stu-id="baca3-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="baca3-140">Tworzenie konta Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="baca3-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="baca3-141">Aby można było utworzyć konto usługi Data Lake Analytics, należy najpierw utworzyć grupę zasobów platformy Azure i konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="baca3-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="baca3-142">Zobacz [Tworzenie konta usługi Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="baca3-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="baca3-143">Następujące polecenie cURL ilustruje sposób utworzenia konta:</span><span class="sxs-lookup"><span data-stu-id="baca3-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="baca3-144">Zastąp \<`REDACTED`\> tokenem autoryzacji, \<`AzureSubscriptionID`\> identyfikatorem subskrypcji, \<`AzureResourceGroupName`\> nazwą istniejącej grupy zasobów platformy Azure i \<`NewAzureDataLakeAnalyticsAccountName`\> nazwą nowego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="baca3-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="baca3-145">Ładunek żądania dla tego polecenia jest zawarty w pliku **CreateDatalakeAnalyticsAccountRequest.json**, który jest udostępniany dla parametru `-d` użytego powyżej.</span><span class="sxs-lookup"><span data-stu-id="baca3-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="baca3-146">Zawartość pliku input.json powinna wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="baca3-146">The contents of the input.json file resemble the following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="baca3-147">Wyświetlanie listy kont usługi Data Lake Analytics w subskrypcji</span><span class="sxs-lookup"><span data-stu-id="baca3-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="baca3-148">Następujące polecenie cURL ilustruje sposób wyświetlenia listy kont w subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="baca3-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="baca3-149">Zastąp \<`REDACTED`\> tokenem autoryzacji, a \<`AzureSubscriptionID`\> identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="baca3-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="baca3-150">Dane wyjściowe są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="baca3-150">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="baca3-151">Uzyskiwanie informacji o koncie usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="baca3-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="baca3-152">Następujące polecenie cURL ilustruje sposób uzyskania informacji o koncie:</span><span class="sxs-lookup"><span data-stu-id="baca3-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="baca3-153">Zastąp \<`REDACTED`\> tokenem autoryzacji, \<`AzureSubscriptionID`\> identyfikatorem subskrypcji, \<`AzureResourceGroupName`\> nazwą istniejącej grupy zasobów platformy Azure i \<`DataLakeAnalyticsAccountName`\> nazwą istniejącego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="baca3-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="baca3-154">Dane wyjściowe są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="baca3-154">The output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="baca3-155">Wyświetlanie listy magazynów usługi Data Lake Store na koncie usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="baca3-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="baca3-156">Następujące polecenie cURL ilustruje sposób wyświetlenia listy magazynów usługi Data Lake Store na koncie:</span><span class="sxs-lookup"><span data-stu-id="baca3-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="baca3-157">Zastąp \<`REDACTED`\> tokenem autoryzacji, \<`AzureSubscriptionID`\> identyfikatorem subskrypcji, \<`AzureResourceGroupName`\> nazwą istniejącej grupy zasobów platformy Azure i \<`DataLakeAnalyticsAccountName`\> nazwą istniejącego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="baca3-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="baca3-158">Dane wyjściowe są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="baca3-158">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="baca3-159">Przesyłanie zadań U-SQL</span><span class="sxs-lookup"><span data-stu-id="baca3-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="baca3-160">Następujące polecenie cURL ilustruje sposób przesłania zadania U-SQL:</span><span class="sxs-lookup"><span data-stu-id="baca3-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="baca3-161">Zastąp \<`REDACTED`\> tokenem autoryzacji, a \<`DataLakeAnalyticsAccountName`\> nazwą istniejącego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="baca3-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="baca3-162">Ładunek żądania dla tego polecenia jest zawarty w pliku **SubmitADLAJob.json**, który jest udostępniany dla parametru `-d` użytego powyżej.</span><span class="sxs-lookup"><span data-stu-id="baca3-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="baca3-163">Zawartość pliku input.json powinna wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="baca3-163">The contents of the input.json file resemble the following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="baca3-164">Dane wyjściowe są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="baca3-164">The output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="baca3-165">Wyświetlenie listy zadań U-SQL</span><span class="sxs-lookup"><span data-stu-id="baca3-165">List U-SQL jobs</span></span>
<span data-ttu-id="baca3-166">Następujące polecenie cURL ilustruje sposób wyświetlenia listy zadań U-SQL:</span><span class="sxs-lookup"><span data-stu-id="baca3-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="baca3-167">Zastąp \<`REDACTED`\> tokenem autoryzacji, a \<`DataLakeAnalyticsAccountName`\> nazwą istniejącego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="baca3-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="baca3-168">Dane wyjściowe są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="baca3-168">The output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="baca3-169">Pobieranie elementów katalogu</span><span class="sxs-lookup"><span data-stu-id="baca3-169">Get catalog items</span></span>
<span data-ttu-id="baca3-170">Następujące polecenie cURL ilustruje sposób pobrania baz danych z katalogu:</span><span class="sxs-lookup"><span data-stu-id="baca3-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="baca3-171">Dane wyjściowe są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="baca3-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="baca3-172">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="baca3-172">See also</span></span>
* <span data-ttu-id="baca3-173">Aby uzyskać informacje na temat bardziej złożonego zapytania, zobacz temat [Analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="baca3-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="baca3-174">Aby rozpocząć tworzenie aplikacji w języku U-SQL, zobacz artykuł [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="baca3-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="baca3-175">Aby dowiedzieć się więcej o języku U-SQL, zobacz [Wprowadzenie do języka U-SQL w usłudze Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="baca3-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="baca3-176">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="baca3-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="baca3-177">Aby zapoznać się z omówieniem usługi Data Lake Analytics, zobacz [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="baca3-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="baca3-178">Aby wyświetlić ten samouczek przy użyciu innych narzędzi, kliknij odpowiedni selektor karty w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="baca3-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

