---
title: "Korzystanie z interfejsu API REST przy rozpoczynaniu pracy z usługą Data Lake Store | Microsoft Docs"
description: "Korzystanie z interfejsów API REST WebHDFS w celu wykonywania operacji w usłudze Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: dc2c8f58e0a2faf1b00f4903148328a5141a8637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="9024e-103">Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="9024e-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9024e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9024e-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="9024e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9024e-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="9024e-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="9024e-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="9024e-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="9024e-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="9024e-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="9024e-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="9024e-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9024e-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="9024e-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="9024e-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="9024e-111">Python</span><span class="sxs-lookup"><span data-stu-id="9024e-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="9024e-112">Z tego artykułu dowiesz się, jak używać interfejsów API REST WebHDFS i interfejsów API REST usługi Data Lake Store w celu zarządzania kontem oraz wykonywania operacji systemu plików w usłudze Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-112">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="9024e-113">Usługa Azure Data Lake Store ujawnia swoje interfejsy API REST w celu wykonywania operacji zarządzania kontem.</span><span class="sxs-lookup"><span data-stu-id="9024e-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="9024e-114">Jednak usługa Data Lake Store jest zgodna z systemem plików HDFS i ekosystemem Hadoop, dlatego umożliwia korzystanie z interfejsów API REST WebHDFS w celu wykonywania operacji systemu plików.</span><span class="sxs-lookup"><span data-stu-id="9024e-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="9024e-115">Aby uzyskać szczegółowe informacje na temat obsługi interfejsu API REST przez usługę Data Lake Store, zobacz [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx) (Dokumentacja interfejsu API REST usługi Azure Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="9024e-115">For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9024e-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9024e-116">Prerequisites</span></span>
* <span data-ttu-id="9024e-117">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="9024e-117">**An Azure subscription**.</span></span> <span data-ttu-id="9024e-118">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9024e-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9024e-119">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9024e-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="9024e-120">Za pomocą aplikacji usługi Azure AD można uwierzytelnić aplikację usługi Data Lake Store w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9024e-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="9024e-121">Istnieją różne metody uwierzytelniania w usłudze Azure AD: **uwierzytelnianie użytkowników końcowych** i **uwierzytelnianie między usługami**.</span><span class="sxs-lookup"><span data-stu-id="9024e-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="9024e-122">Instrukcje i dodatkowe informacje na temat uwierzytelniania można znaleźć w następujących artykułach: [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) (Uwierzytelnianie użytkowników końcowych) lub [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md) (Uwierzytelnianie między usługami).</span><span class="sxs-lookup"><span data-stu-id="9024e-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="9024e-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="9024e-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="9024e-124">W tym artykule jest używane narzędzie cURL w celu zademonstrowania sposobu wykonywania wywołań interfejsu API REST względem konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-124">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="9024e-125">W jaki sposób uwierzytelniać za pomocą usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9024e-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="9024e-126">Dostępne są dwa podejścia do uwierzytelniania za pomocą usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9024e-126">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="9024e-127">Uwierzytelnianie użytkowników końcowych (interakcyjne)</span><span class="sxs-lookup"><span data-stu-id="9024e-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="9024e-128">W tym scenariuszu aplikacja wyświetla monit o zalogowanie się i wówczas wszystkie operacje są wykonywane w kontekście zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9024e-128">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="9024e-129">Wykonaj następujące kroki, aby przeprowadzić uwierzytelnianie interakcyjne.</span><span class="sxs-lookup"><span data-stu-id="9024e-129">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="9024e-130">Za pomocą aplikacji przekieruj użytkownika pod następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="9024e-130">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="9024e-131">Identyfikator \<REDIRECT-URI> musi być zakodowany na potrzeby adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9024e-131">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="9024e-132">Dlatego w celu zapisania adresu https://localhost użyj ciągu `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="9024e-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="9024e-133">Na potrzeby tego samouczka możesz zastąpić symbole zastępcze w powyższym adresie URL i wkleić go w pasku adresu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="9024e-133">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="9024e-134">Nastąpi przekierowanie w celu uwierzytelniania przy użyciu identyfikatora logowania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9024e-134">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="9024e-135">Gdy pomyślnie się zalogujesz, odpowiedź zostanie wyświetlona na pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="9024e-135">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="9024e-136">Odpowiedź będzie miała następujący format:</span><span class="sxs-lookup"><span data-stu-id="9024e-136">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="9024e-137">Przechwyć kod autoryzacji z odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9024e-137">Capture the authorization code from the response.</span></span> <span data-ttu-id="9024e-138">W ramach niniejszego samouczka możesz skopiować kod autoryzacji z paska adresu przeglądarki sieci web i przekazać go w żądaniu POST do punktu końcowego tokenu w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="9024e-138">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="9024e-139">W takim przypadku identyfikatora \<REDIRECT-URI> nie trzeba kodować.</span><span class="sxs-lookup"><span data-stu-id="9024e-139">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="9024e-140">Odpowiedzią jest obiekt JSON, który zawiera token dostępu (np. `"access_token": "<ACCESS_TOKEN>"`) oraz token odświeżania (np. `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="9024e-140">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="9024e-141">Aplikacja używa tokenu dostępu podczas uzyskiwania dostępu do usługi Azure Data Lake Store i tokenu odświeżania, aby uzyskać inny token dostępu w przypadku wygaśnięcia tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9024e-141">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="9024e-142">Po wygaśnięciu tokenu dostępu możesz zażądać nowego tokenu dostępu, używając tokenu odświeżania w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="9024e-142">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="9024e-143">Więcej informacji na temat interakcyjnego uwierzytelniania użytkownika zawiera temat [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx) (Przepływ udzielania kodu autoryzacji).</span><span class="sxs-lookup"><span data-stu-id="9024e-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="9024e-144">Uwierzytelnianie między usługami (nieinterakcyjne)</span><span class="sxs-lookup"><span data-stu-id="9024e-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="9024e-145">W tym scenariuszu aplikacja udostępnia własne poświadczenia, aby wykonywać operacje.</span><span class="sxs-lookup"><span data-stu-id="9024e-145">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="9024e-146">W tym celu należy wygenerować żądanie POST, tak jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="9024e-146">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="9024e-147">Dane wyjściowe tego żądania będą zawierać token autoryzacji (oznaczony jako `access-token` w danych wyjściowych poniżej), który następnie będzie przekazywany w wywołaniach interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="9024e-147">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="9024e-148">Zapisz ten token uwierzytelniania w pliku tekstowym. Będzie on potrzebny w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="9024e-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="9024e-149">W tym artykule wykorzystano podejście **nieinterakcyjne**.</span><span class="sxs-lookup"><span data-stu-id="9024e-149">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="9024e-150">Więcej informacji na temat podejścia nieinterakcyjnego (wywołań między usługami) zawiera temat [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx) (Wywołania między usługami przy użyciu poświadczeń).</span><span class="sxs-lookup"><span data-stu-id="9024e-150">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="9024e-151">Tworzenie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="9024e-152">Ta operacja jest oparta na wywołaniu interfejsu API REST zdefiniowanym [tutaj](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="9024e-152">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="9024e-153">Użyj następującego polecenia cURL.</span><span class="sxs-lookup"><span data-stu-id="9024e-153">Use the following cURL command.</span></span> <span data-ttu-id="9024e-154">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="9024e-155">W poleceniu powyżej zastąp ciąg \<`REDACTED`\> tokenem autoryzacji pobranym wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9024e-155">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="9024e-156">Ładunek żądania dla tego polecenia jest zawarty w pliku **input.json**, który jest udostępniany dla parametru `-d` powyżej.</span><span class="sxs-lookup"><span data-stu-id="9024e-156">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="9024e-157">Zawartość pliku input.json powinna wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9024e-157">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="9024e-158">Tworzenie folderów w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="9024e-159">Ta operacja jest oparta na wywołaniu interfejsu API REST WebHDFS zdefiniowanym [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="9024e-159">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="9024e-160">Użyj następującego polecenia cURL.</span><span class="sxs-lookup"><span data-stu-id="9024e-160">Use the following cURL command.</span></span> <span data-ttu-id="9024e-161">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="9024e-162">W poleceniu powyżej zastąp ciąg \<`REDACTED`\> tokenem autoryzacji pobranym wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9024e-162">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="9024e-163">To polecenie tworzy katalog o nazwie **mytempdir** w folderze głównym Twojego konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-163">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="9024e-164">Jeśli operacja zakończy się pomyślnie, powinna pojawić się odpowiedź podobna do poniższej:</span><span class="sxs-lookup"><span data-stu-id="9024e-164">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="9024e-165">Wyświetlanie listy folderów w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="9024e-166">Ta operacja jest oparta na wywołaniu interfejsu API REST WebHDFS zdefiniowanym [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="9024e-166">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="9024e-167">Użyj następującego polecenia cURL.</span><span class="sxs-lookup"><span data-stu-id="9024e-167">Use the following cURL command.</span></span> <span data-ttu-id="9024e-168">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="9024e-169">W poleceniu powyżej zastąp ciąg \<`REDACTED`\> tokenem autoryzacji pobranym wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9024e-169">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="9024e-170">Jeśli operacja zakończy się pomyślnie, powinna pojawić się odpowiedź podobna do poniższej:</span><span class="sxs-lookup"><span data-stu-id="9024e-170">You should see a response like this if the operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="9024e-171">Przekazywanie danych do konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="9024e-172">Ta operacja jest oparta na wywołaniu interfejsu API REST WebHDFS zdefiniowanym [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="9024e-172">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="9024e-173">Użyj następującego polecenia cURL.</span><span class="sxs-lookup"><span data-stu-id="9024e-173">Use the following cURL command.</span></span> <span data-ttu-id="9024e-174">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="9024e-175">W powyższej składni parametr **-T** wskazuje na lokalizację przekazywanego pliku.</span><span class="sxs-lookup"><span data-stu-id="9024e-175">In the above syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="9024e-176">Dane wyjściowe będą podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9024e-176">The output is similar to the following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="9024e-177">Odczytywanie danych z konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="9024e-178">Ta operacja jest oparta na wywołaniu interfejsu API REST WebHDFS zdefiniowanym [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="9024e-178">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="9024e-179">Odczytywanie danych z konta usługi Data Lake Store jest procesem dwuetapowym.</span><span class="sxs-lookup"><span data-stu-id="9024e-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="9024e-180">Najpierw prześlij żądanie GET względem punktu końcowego `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="9024e-180">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="9024e-181">To spowoduje zwrócenie lokalizacji, do której należy przesłać kolejne żądanie GET.</span><span class="sxs-lookup"><span data-stu-id="9024e-181">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="9024e-182">Następnie prześlij żądanie GET względem punktu końcowego `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="9024e-182">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="9024e-183">Zostanie wyświetlona zawartość pliku.</span><span class="sxs-lookup"><span data-stu-id="9024e-183">This will display the contents of the file.</span></span>

<span data-ttu-id="9024e-184">Jednak ponieważ nie ma żadnej różnicy w parametrach wejściowych kroku pierwszego i drugiego, możesz użyć parametru `-L` w celu przesłania pierwszego żądania.</span><span class="sxs-lookup"><span data-stu-id="9024e-184">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="9024e-185">`-L` — ta opcja w praktyce łączy dwa żądania w jedno i powoduje, że narzędzie cURL ponowi żądanie dla nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="9024e-185">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="9024e-186">Na koniec zostaną wyświetlone dane wyjściowe z wszystkich wywołań żądań, tak jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="9024e-186">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="9024e-187">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="9024e-188">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9024e-188">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="9024e-189">Zmiana nazwy pliku w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="9024e-190">Ta operacja jest oparta na wywołaniu interfejsu API REST WebHDFS zdefiniowanym [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="9024e-190">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="9024e-191">Użyj następującego polecenia cURL, aby zmienić nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="9024e-191">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="9024e-192">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="9024e-193">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9024e-193">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="9024e-194">Usuwanie pliku z konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="9024e-195">Ta operacja jest oparta na wywołaniu interfejsu API REST WebHDFS zdefiniowanym [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="9024e-195">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="9024e-196">Użyj następującego polecenia cURL, aby usunąć plik.</span><span class="sxs-lookup"><span data-stu-id="9024e-196">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="9024e-197">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="9024e-198">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9024e-198">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="9024e-199">Usuwanie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9024e-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="9024e-200">Ta operacja jest oparta na wywołaniu interfejsu API REST zdefiniowanym [tutaj](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="9024e-200">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="9024e-201">Użyj poniższego polecenia cURL, aby usunąć konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-201">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="9024e-202">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9024e-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="9024e-203">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9024e-203">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="9024e-204">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9024e-204">See also</span></span>
* <span data-ttu-id="9024e-205">[Open Source Big Data applications compatible with Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md) (Aplikacje danych big data typu open source zgodne z usługą Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="9024e-205">[Open Source Big Data applications compatible with Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md)</span></span>

