---
title: "wprowadzenie do usługi Data Lake Store tooget interfejsu API REST hello aaaUse | Dokumentacja firmy Microsoft"
description: "Używać interfejsów API REST WebHDFS tooperform operacji w usłudze Data Lake Store"
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
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="1db56-103">Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="1db56-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1db56-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1db56-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1db56-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1db56-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1db56-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1db56-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1db56-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="1db56-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1db56-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="1db56-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1db56-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1db56-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1db56-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1db56-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1db56-111">Python</span><span class="sxs-lookup"><span data-stu-id="1db56-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="1db56-112">W tym artykule dowiesz się, jak toouse interfejsów API REST WebHDFS i Data Lake magazynu REST API tooperform konto zarządzania, a także operacji systemu plików w usłudze Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="1db56-113">Usługa Azure Data Lake Store ujawnia swoje interfejsy API REST w celu wykonywania operacji zarządzania kontem.</span><span class="sxs-lookup"><span data-stu-id="1db56-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="1db56-114">Jednak usługa Data Lake Store jest zgodna z systemem plików HDFS i ekosystemem Hadoop, dlatego umożliwia korzystanie z interfejsów API REST WebHDFS w celu wykonywania operacji systemu plików.</span><span class="sxs-lookup"><span data-stu-id="1db56-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="1db56-115">Aby uzyskać szczegółowe informacje na powitania Obsługa interfejsu API REST usługi Data Lake Store, zobacz [dokumentacja interfejsu API REST magazynu Azure Data Lake](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="1db56-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1db56-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1db56-116">Prerequisites</span></span>
* <span data-ttu-id="1db56-117">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="1db56-117">**An Azure subscription**.</span></span> <span data-ttu-id="1db56-118">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1db56-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1db56-119">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1db56-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="1db56-120">Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Store aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1db56-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="1db56-121">Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="1db56-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1db56-122">Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1db56-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="1db56-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="1db56-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="1db56-124">W tym artykule wykorzystano toodemonstrate cURL jak wywołuje toomake interfejsu API REST względem konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="1db56-125">W jaki sposób uwierzytelniać za pomocą usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1db56-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="1db56-126">Możesz użyć dwóch tooauthenticate podejścia przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1db56-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="1db56-127">Uwierzytelnianie użytkowników końcowych (interakcyjne)</span><span class="sxs-lookup"><span data-stu-id="1db56-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="1db56-128">W tym scenariuszu aplikacja hello monituje hello toolog użytkownika w i wszystkie operacje hello są wykonywane w kontekście hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1db56-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="1db56-129">Wykonaj następujące kroki, aby przeprowadzić uwierzytelnianie interakcyjne hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="1db56-130">Za pomocą aplikacji Przekieruj toohello użytkownika hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="1db56-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="1db56-131">\<Identyfikator URI PRZEKIEROWANIA > musi toobe zakodowanego do użycia w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="1db56-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="1db56-132">Dlatego w celu zapisania adresu https://localhost użyj ciągu `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="1db56-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="1db56-133">Hello w celu tego samouczka możesz zastąpić symbole zastępcze hello w adresie URL hello powyżej i wklej go w pasku adresu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="1db56-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="1db56-134">Będzie przekierowany tooauthenticate przy użyciu logowania do systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="1db56-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="1db56-135">Po pomyślnym zalogowaniu odpowiedź hello jest wyświetlany w pasku adresu przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="1db56-136">odpowiedź Hello będą hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="1db56-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="1db56-137">Przechwyć hello kod autoryzacji z odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="1db56-138">W tym samouczku możesz skopiować kod autoryzacji hello z paska adresu przeglądarki sieci web hello hello i przekazać go w hello POST żądania toohello punktu końcowego tokena, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="1db56-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="1db56-139">W takim przypadku hello \<REDIRECT-URI > nie trzeba kodować.</span><span class="sxs-lookup"><span data-stu-id="1db56-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="1db56-140">odpowiedź Hello jest obiekt JSON, który zawiera token dostępu (np. `"access_token": "<ACCESS_TOKEN>"`) oraz token odświeżania (np. `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="1db56-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="1db56-141">Aplikacja używa tokenu dostępu hello podczas uzyskiwania dostępu do usługi Azure Data Lake Store i tooget token odświeżania hello inny token dostępu po wygaśnięciu tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1db56-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="1db56-142">Po wygaśnięciu tokenu dostępu hello mogą żądać tokenu dostępu przy użyciu tokenu odświeżania hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="1db56-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="1db56-143">Więcej informacji na temat interakcyjnego uwierzytelniania użytkownika zawiera temat [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx) (Przepływ udzielania kodu autoryzacji).</span><span class="sxs-lookup"><span data-stu-id="1db56-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="1db56-144">Uwierzytelnianie między usługami (nieinterakcyjne)</span><span class="sxs-lookup"><span data-stu-id="1db56-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="1db56-145">W tym scenariuszu hello hello aplikacja udostępnia własne poświadczenia tooperform hello operacji.</span><span class="sxs-lookup"><span data-stu-id="1db56-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="1db56-146">W tym celu należy wygenerować żądanie POST, takich jak hello przedstawionego poniżej.</span><span class="sxs-lookup"><span data-stu-id="1db56-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="1db56-147">Witaj dane wyjściowe tego żądania będą zawierać token autoryzacji (wskazywane przez `access-token` w danych wyjściowych hello poniżej), który można następnie będzie przekazywany w wywołaniach interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="1db56-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="1db56-148">Zapisz ten token uwierzytelniania w pliku tekstowym. Będzie on potrzebny w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="1db56-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="1db56-149">W tym artykule wykorzystano hello **nieinterakcyjnym** podejście.</span><span class="sxs-lookup"><span data-stu-id="1db56-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="1db56-150">Aby uzyskać więcej informacji na podejścia nieinterakcyjnego (wywołań service-to-service), zobacz [wywołania tooservice przy użyciu poświadczeń usługi](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="1db56-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1db56-151">Tworzenie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="1db56-152">Ta operacja jest oparta na wywołania interfejsu API REST hello zdefiniowane [tutaj](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="1db56-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="1db56-153">Użyj następującego polecenia cURL hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-153">Use hello following cURL command.</span></span> <span data-ttu-id="1db56-154">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="1db56-155">W hello powyżej polecenia, Zastąp \< `REDACTED` \> hello tokenem autoryzacji pobranym wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1db56-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="1db56-156">Witaj ładunku żądania dla tego polecenia jest zawarty w hello **input.json** pliku dostarczonego dla hello `-d` parametru powyżej.</span><span class="sxs-lookup"><span data-stu-id="1db56-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="1db56-157">Witaj zawartość pliku input.json hello przypominać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="1db56-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="1db56-158">Tworzenie folderów w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="1db56-159">Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="1db56-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="1db56-160">Użyj następującego polecenia cURL hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-160">Use hello following cURL command.</span></span> <span data-ttu-id="1db56-161">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="1db56-162">W hello powyżej polecenia, Zastąp \< `REDACTED` \> hello tokenem autoryzacji pobranym wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1db56-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="1db56-163">To polecenie tworzy katalog o nazwie **mytempdir** w folderze głównym hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="1db56-164">Powinny pojawić się odpowiedź podobna Jeśli hello operacja zakończy się pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="1db56-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="1db56-165">Wyświetlanie listy folderów w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="1db56-166">Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="1db56-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="1db56-167">Użyj następującego polecenia cURL hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-167">Use hello following cURL command.</span></span> <span data-ttu-id="1db56-168">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="1db56-169">W hello powyżej polecenia, Zastąp \< `REDACTED` \> hello tokenem autoryzacji pobranym wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1db56-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="1db56-170">Powinny pojawić się odpowiedź podobna Jeśli hello operacja zakończy się pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="1db56-170">You should see a response like this if hello operation completes successfully:</span></span>

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

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="1db56-171">Przekazywanie danych do konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="1db56-172">Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="1db56-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="1db56-173">Użyj następującego polecenia cURL hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-173">Use hello following cURL command.</span></span> <span data-ttu-id="1db56-174">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="1db56-175">W hello powyżej składni **-T** parametr jest hello lokalizację pliku hello podczas przekazywania.</span><span class="sxs-lookup"><span data-stu-id="1db56-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="1db56-176">dane wyjściowe Hello są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1db56-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="1db56-177">Odczytywanie danych z konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="1db56-178">Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="1db56-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="1db56-179">Odczytywanie danych z konta usługi Data Lake Store jest procesem dwuetapowym.</span><span class="sxs-lookup"><span data-stu-id="1db56-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="1db56-180">Najpierw Prześlij żądanie GET względem punktu końcowego hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="1db56-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="1db56-181">Spowoduje to przywrócenie lokalizacji toosubmit hello kolejne żądanie GET.</span><span class="sxs-lookup"><span data-stu-id="1db56-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="1db56-182">Następnie przesłać hello żądanie GET względem punktu końcowego hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="1db56-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="1db56-183">Spowoduje to wyświetlenie hello zawartość pliku hello.</span><span class="sxs-lookup"><span data-stu-id="1db56-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="1db56-184">Jednakże, ponieważ nie ma żadnej różnicy w hello parametrów wejściowych między hello najpierw i hello w drugim kroku, możesz użyć hello `-L` parametru toosubmit hello pierwszego żądania.</span><span class="sxs-lookup"><span data-stu-id="1db56-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="1db56-185">`-L`Opcja zasadniczo łączy dwa żądania w jednym i spowoduje, że narzędzie cURL ponowi Żądanie hello na powitania nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="1db56-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="1db56-186">Na koniec hello dane wyjściowe wszystkich wywołań żądań hello jest wyświetlana, tak samo, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="1db56-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="1db56-187">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="1db56-188">Powinny być widoczne następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="1db56-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="1db56-189">Zmiana nazwy pliku w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="1db56-190">Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="1db56-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="1db56-191">Użyj następujących hello cURL toorename polecenia pliku.</span><span class="sxs-lookup"><span data-stu-id="1db56-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="1db56-192">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="1db56-193">Powinny być widoczne następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="1db56-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="1db56-194">Usuwanie pliku z konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="1db56-195">Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="1db56-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="1db56-196">Użyj następujących hello cURL toodelete polecenia pliku.</span><span class="sxs-lookup"><span data-stu-id="1db56-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="1db56-197">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="1db56-198">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="1db56-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="1db56-199">Usuwanie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1db56-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="1db56-200">Ta operacja jest oparta na wywołania interfejsu API REST hello zdefiniowane [tutaj](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="1db56-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="1db56-201">Użyj następujących hello cURL toodelete polecenia konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="1db56-202">Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1db56-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="1db56-203">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="1db56-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="1db56-204">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1db56-204">See also</span></span>
* <span data-ttu-id="1db56-205">[Open Source Big Data applications compatible with Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md) (Aplikacje danych big data typu open source zgodne z usługą Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="1db56-205">[Open Source Big Data applications compatible with Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md)</span></span>

