---
title: "aaaGet wprowadzenie do usługi Data Lake Analytics przy użyciu interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Użyj interfejsów API REST WebHDFS tooperform operacji na usługi Data Lake Analytics"
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
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="a30cd-103">Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="a30cd-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="a30cd-104">Dowiedz się, jak toouse interfejsów API REST WebHDFS i Data Lake Analytics REST API toomanage usługi Data Lake Analytics kont, zadania i w katalogu.</span><span class="sxs-lookup"><span data-stu-id="a30cd-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a30cd-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a30cd-105">Prerequisites</span></span>
* <span data-ttu-id="a30cd-106">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="a30cd-106">**An Azure subscription**.</span></span> <span data-ttu-id="a30cd-107">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a30cd-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a30cd-108">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a30cd-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="a30cd-109">Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Analytics aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a30cd-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="a30cd-110">Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="a30cd-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a30cd-111">Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniony przez usługi Data Lake Analytics przy użyciu usługi Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a30cd-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="a30cd-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="a30cd-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="a30cd-113">W tym artykule wykorzystano toodemonstrate cURL jak wywołuje toomake interfejsu API REST względem konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a30cd-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="a30cd-114">Uwierzytelnianie za pomocą usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a30cd-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="a30cd-115">Istnieją dwie metody uwierzytelniania za pomocą usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a30cd-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="a30cd-116">Uwierzytelnianie użytkowników końcowych (interakcyjne)</span><span class="sxs-lookup"><span data-stu-id="a30cd-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="a30cd-117">Za pomocą tej metody, aplikacja wyświetli monit hello toolog użytkownika w i wszystkie operacje hello są wykonywane w kontekście hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a30cd-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="a30cd-118">Wykonaj następujące kroki, aby przeprowadzić uwierzytelnianie interakcyjne:</span><span class="sxs-lookup"><span data-stu-id="a30cd-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="a30cd-119">Za pomocą aplikacji Przekieruj toohello użytkownika hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="a30cd-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="a30cd-120">\<Identyfikator URI PRZEKIEROWANIA > musi toobe zakodowanego do użycia w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="a30cd-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="a30cd-121">Dlatego w celu zapisania adresu https://localhost użyj ciągu `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="a30cd-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="a30cd-122">Hello w celu tego samouczka możesz zastąpić symbole zastępcze hello w adresie URL hello powyżej i wklej go w pasku adresu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="a30cd-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="a30cd-123">Będzie przekierowany tooauthenticate przy użyciu logowania do systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="a30cd-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="a30cd-124">Gdy pomyślnie się zalogujesz, odpowiedź hello jest wyświetlany w pasku adresu przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="a30cd-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="a30cd-125">odpowiedź Hello będą hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="a30cd-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="a30cd-126">Przechwyć hello kod autoryzacji z odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="a30cd-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="a30cd-127">W tym samouczku możesz skopiować kod autoryzacji hello z paska adresu przeglądarki sieci web hello hello i przekazać go w hello POST żądania toohello punktu końcowego tokena, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="a30cd-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="a30cd-128">W takim przypadku hello \<REDIRECT-URI > nie trzeba kodować.</span><span class="sxs-lookup"><span data-stu-id="a30cd-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="a30cd-129">odpowiedź Hello jest obiekt JSON, który zawiera token dostępu (np. `"access_token": "<ACCESS_TOKEN>"`) oraz token odświeżania (np. `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="a30cd-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="a30cd-130">Aplikacja używa tokenu dostępu hello podczas uzyskiwania dostępu do usługi Azure Data Lake Store i tooget token odświeżania hello inny token dostępu po wygaśnięciu tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a30cd-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="a30cd-131">Po wygaśnięciu tokenu dostępu hello mogą żądać tokenu dostępu przy użyciu tokenu odświeżania hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="a30cd-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="a30cd-132">Więcej informacji na temat interakcyjnego uwierzytelniania użytkownika zawiera temat [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx) (Przepływ udzielania kodu autoryzacji).</span><span class="sxs-lookup"><span data-stu-id="a30cd-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="a30cd-133">Uwierzytelnianie między usługami (nieinterakcyjne)</span><span class="sxs-lookup"><span data-stu-id="a30cd-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="a30cd-134">Metoda ta aplikacja udostępnia własne poświadczenia tooperform hello operacji.</span><span class="sxs-lookup"><span data-stu-id="a30cd-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="a30cd-135">W tym celu należy wygenerować żądanie POST, tak jak pokazano poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="a30cd-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="a30cd-136">Witaj dane wyjściowe tego żądania będą zawierać token autoryzacji (wskazywane przez `access-token` w danych wyjściowych hello poniżej), który można następnie będzie przekazywany w wywołaniach interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a30cd-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="a30cd-137">Zapisz ten token uwierzytelniania w pliku tekstowym. Będzie on potrzebny w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="a30cd-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="a30cd-138">W tym artykule wykorzystano hello **nieinterakcyjnym** podejście.</span><span class="sxs-lookup"><span data-stu-id="a30cd-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="a30cd-139">Aby uzyskać więcej informacji na podejścia nieinterakcyjnego (wywołań service-to-service), zobacz [wywołania tooservice przy użyciu poświadczeń usługi](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="a30cd-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="a30cd-140">Tworzenie konta Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a30cd-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="a30cd-141">Aby można było utworzyć konto usługi Data Lake Analytics, należy najpierw utworzyć grupę zasobów platformy Azure i konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a30cd-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="a30cd-142">Zobacz [Tworzenie konta usługi Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="a30cd-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="a30cd-143">Witaj, jak po pokazuje polecenia Curl toocreate konta:</span><span class="sxs-lookup"><span data-stu-id="a30cd-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="a30cd-144">Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z Identyfikatorem subskrypcji \< `AzureResourceGroupName` \> z istniejącym zasobem platformy Azure Nazwa grupy i \< `NewAzureDataLakeAnalyticsAccountName` \> z nową nazwą konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a30cd-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="a30cd-145">Witaj ładunku żądania dla tego polecenia jest zawarty w hello **CreateDatalakeAnalyticsAccountRequest.json** pliku dostarczonego dla hello `-d` parametru powyżej.</span><span class="sxs-lookup"><span data-stu-id="a30cd-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="a30cd-146">Witaj zawartość pliku input.json hello przypominać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a30cd-146">hello contents of hello input.json file resemble hello following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="a30cd-147">Wyświetlanie listy kont usługi Data Lake Analytics w subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a30cd-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="a30cd-148">Witaj następującego polecenia Curl pokazuje, jak toolist kont w ramach subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="a30cd-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="a30cd-149">Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z identyfikatorem subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a30cd-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="a30cd-150">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="a30cd-150">hello output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="a30cd-151">Uzyskiwanie informacji o koncie usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a30cd-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="a30cd-152">Witaj, jak po pokazuje polecenia Curl tooget informacje o koncie:</span><span class="sxs-lookup"><span data-stu-id="a30cd-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="a30cd-153">Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z Identyfikatorem subskrypcji \< `AzureResourceGroupName` \> z istniejącym zasobem platformy Azure Nazwa grupy i \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a30cd-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="a30cd-154">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="a30cd-154">hello output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="a30cd-155">Wyświetlanie listy magazynów usługi Data Lake Store na koncie usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a30cd-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="a30cd-156">Witaj następującego polecenia Curl pokazuje, jak magazyny toolist Data Lake konta:</span><span class="sxs-lookup"><span data-stu-id="a30cd-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="a30cd-157">Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z Identyfikatorem subskrypcji \< `AzureResourceGroupName` \> z istniejącym zasobem platformy Azure Nazwa grupy i \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a30cd-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="a30cd-158">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="a30cd-158">hello output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="a30cd-159">Przesyłanie zadań U-SQL</span><span class="sxs-lookup"><span data-stu-id="a30cd-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="a30cd-160">Witaj, jak po pokazuje polecenia Curl zadania toosubmit U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a30cd-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="a30cd-161">Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a30cd-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="a30cd-162">Witaj ładunku żądania dla tego polecenia jest zawarty w hello **SubmitADLAJob.json** pliku dostarczonego dla hello `-d` parametru powyżej.</span><span class="sxs-lookup"><span data-stu-id="a30cd-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="a30cd-163">Witaj zawartość pliku input.json hello przypominać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a30cd-163">hello contents of hello input.json file resemble hello following:</span></span>

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="a30cd-164">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="a30cd-164">hello output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="a30cd-165">Wyświetlenie listy zadań U-SQL</span><span class="sxs-lookup"><span data-stu-id="a30cd-165">List U-SQL jobs</span></span>
<span data-ttu-id="a30cd-166">Witaj, jak po pokazuje polecenia Curl zadania toolist U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a30cd-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="a30cd-167">Zastąp \< `REDACTED` \> tokenem autoryzacji hello i \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a30cd-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="a30cd-168">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="a30cd-168">hello output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="a30cd-169">Pobieranie elementów katalogu</span><span class="sxs-lookup"><span data-stu-id="a30cd-169">Get catalog items</span></span>
<span data-ttu-id="a30cd-170">Witaj następującego polecenia Curl pokazuje, jak bazy danych hello tooget z hello katalogu:</span><span class="sxs-lookup"><span data-stu-id="a30cd-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="a30cd-171">Witaj wynik jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="a30cd-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="a30cd-172">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a30cd-172">See also</span></span>
* <span data-ttu-id="a30cd-173">toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="a30cd-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="a30cd-174">tooget Rozpoczęto tworzenie aplikacji U-SQL, zobacz [skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a30cd-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="a30cd-175">toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a30cd-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="a30cd-176">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a30cd-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="a30cd-177">Zobacz tooget Przegląd usługi Data Lake Analytics [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a30cd-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="a30cd-178">toosee hello sam samouczek przy użyciu innych narzędzi, kliknij przycisk hello selektor karty w górnej części hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="a30cd-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

