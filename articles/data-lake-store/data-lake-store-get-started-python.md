---
title: "wprowadzenie do usługi Azure Data Lake Store aaaUse hello zestaw SDK Python tooget | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toowork zestaw SDK Python z konta usługi Data Lake Store i hello systemu plików."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="59684-103">Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="59684-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="59684-104">Portal</span><span class="sxs-lookup"><span data-stu-id="59684-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="59684-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59684-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="59684-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="59684-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="59684-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="59684-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="59684-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="59684-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="59684-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="59684-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="59684-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="59684-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="59684-111">Python</span><span class="sxs-lookup"><span data-stu-id="59684-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="59684-112">Dowiedz się jak toouse hello zestaw SDK Python platformy Azure i usługi Azure Data Lake Store tooperform podstawowe operacje takie jak tworzenie folderów, przekazywanie i pobieranie plików danych itp. Aby uzyskać więcej informacji o usłudze Data Lake, zobacz temat [Usługa Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59684-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59684-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59684-113">Prerequisites</span></span>

* <span data-ttu-id="59684-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="59684-114">**Python**.</span></span> <span data-ttu-id="59684-115">Możesz pobrać środowisko Python [tutaj](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="59684-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="59684-116">W tym artykule używany jest język Python 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="59684-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="59684-117">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="59684-117">**An Azure subscription**.</span></span> <span data-ttu-id="59684-118">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59684-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="59684-119">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="59684-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="59684-120">Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Store aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="59684-121">Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="59684-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="59684-122">Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="59684-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="59684-123">Instalowanie modułów hello</span><span class="sxs-lookup"><span data-stu-id="59684-123">Install hello modules</span></span>

<span data-ttu-id="59684-124">toowork z Data Lake Store z użyciem języka Python, należy tooinstall trzech modułów.</span><span class="sxs-lookup"><span data-stu-id="59684-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="59684-125">Witaj `azure-mgmt-resource` modułu.</span><span class="sxs-lookup"><span data-stu-id="59684-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="59684-126">Obejmuje to moduły platformy Azure dla usługi Active Directory itp.</span><span class="sxs-lookup"><span data-stu-id="59684-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="59684-127">Witaj `azure-mgmt-datalake-store` modułu.</span><span class="sxs-lookup"><span data-stu-id="59684-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="59684-128">W tym operacji zarządzania kontem usługi Azure Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="59684-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="59684-129">Aby uzyskać więcej informacji na temat tego modułu, zobacz [dokumentację modułu do zarządzania dla usługi Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="59684-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="59684-130">Witaj `azure-datalake-store` modułu.</span><span class="sxs-lookup"><span data-stu-id="59684-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="59684-131">W tym hello Azure Data Lake Store wykonywania operacji systemu plików.</span><span class="sxs-lookup"><span data-stu-id="59684-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="59684-132">Aby uzyskać więcej informacji na temat tego modułu, zobacz [dokumentację modułu systemu plików dla usługi Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="59684-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="59684-133">Użyj następujących hello polecenia tooinstall hello modułów.</span><span class="sxs-lookup"><span data-stu-id="59684-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="59684-134">Tworzenie nowej aplikacji w języku Python</span><span class="sxs-lookup"><span data-stu-id="59684-134">Create a new Python application</span></span>

1. <span data-ttu-id="59684-135">W hello IDE wyboru Utwórz nową aplikację języka Python, na przykład **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="59684-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="59684-136">Dodaj następujące wiersze tooimport hello wymagane moduły hello</span><span class="sxs-lookup"><span data-stu-id="59684-136">Add hello following lines tooimport hello required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="59684-137">Zapisz zmiany toomysample.py.</span><span class="sxs-lookup"><span data-stu-id="59684-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="59684-138">Authentication</span><span class="sxs-lookup"><span data-stu-id="59684-138">Authentication</span></span>

<span data-ttu-id="59684-139">W tej sekcji są omawiane tooauthenticate różne sposoby hello z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="59684-140">dostępne opcje Hello to:</span><span class="sxs-lookup"><span data-stu-id="59684-140">hello options available are:</span></span>

* <span data-ttu-id="59684-141">Uwierzytelnianie użytkowników końcowych</span><span class="sxs-lookup"><span data-stu-id="59684-141">End-user authentication</span></span>
* <span data-ttu-id="59684-142">Uwierzytelnianie między usługami</span><span class="sxs-lookup"><span data-stu-id="59684-142">Service-to-service authentication</span></span>
* <span data-ttu-id="59684-143">Uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="59684-143">Multi-factor authentication</span></span>

<span data-ttu-id="59684-144">Te opcje uwierzytelnianie muszą być używane dla modułów zarządzania kontami i zarządzania systemem plików.</span><span class="sxs-lookup"><span data-stu-id="59684-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="59684-145">Uwierzytelnianie użytkowników końcowych w celu zarządzania kontami</span><span class="sxs-lookup"><span data-stu-id="59684-145">End-user authentication for account management</span></span>

<span data-ttu-id="59684-146">Ta tooauthenticate za pomocą usługi Azure AD dla operacji zarządzania kontem (Tworzenie/usuwanie konta usługi Data Lake Store itp.).</span><span class="sxs-lookup"><span data-stu-id="59684-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="59684-147">Należy podać nazwę i hasło użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="59684-148">Należy pamiętać, że użytkownik hello nie powinno być skonfigurowane dla usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="59684-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="59684-149">Uwierzytelnianie użytkowników końcowych dla operacji systemu plików</span><span class="sxs-lookup"><span data-stu-id="59684-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="59684-150">Ta tooauthenticate za pomocą usługi Azure AD w celu wykonywania operacji (Tworzenie folderów, przekazywanie plików itp.).</span><span class="sxs-lookup"><span data-stu-id="59684-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="59684-151">Użyj tej metody wraz z istniejącą natywną aplikacją **kliencką** usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="59684-152">Podaj poświadczenia dla użytkownika Hello Azure AD nie powinno być skonfigurowane dla usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="59684-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="59684-153">Uwierzytelnianie między usługami z kluczem tajnym klienta w celu zarządzania kontami</span><span class="sxs-lookup"><span data-stu-id="59684-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="59684-154">Ta tooauthenticate za pomocą usługi Azure AD dla operacji zarządzania kontem (Tworzenie/usuwanie konta usługi Data Lake Store itp.).</span><span class="sxs-lookup"><span data-stu-id="59684-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="59684-155">Witaj następujący fragment kodu mogą być używane tooauthenticate aplikacji nieinteraktywnie, przy użyciu klucza tajnego powitania klienta dla aplikacji / usługi podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="59684-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="59684-156">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="59684-157">Uwierzytelnianie między usługami z wpisem tajnym klienta dla operacji systemu plików</span><span class="sxs-lookup"><span data-stu-id="59684-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="59684-158">Ta tooauthenticate za pomocą usługi Azure AD w celu wykonywania operacji (Tworzenie folderów, przekazywanie plików itp.).</span><span class="sxs-lookup"><span data-stu-id="59684-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="59684-159">Witaj następujący fragment kodu mogą być używane tooauthenticate aplikacji nieinteraktywnie, przy użyciu klucza tajnego powitania klienta dla aplikacji / usługi podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="59684-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="59684-160">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="59684-161">Uwierzytelnianie wieloskładnikowe w celu zarządzania kontami</span><span class="sxs-lookup"><span data-stu-id="59684-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="59684-162">Ta tooauthenticate za pomocą usługi Azure AD dla operacji zarządzania kontem (Tworzenie/usuwanie konta usługi Data Lake Store itp.).</span><span class="sxs-lookup"><span data-stu-id="59684-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="59684-163">Witaj następujący fragment kodu może być używany tooauthenticate aplikację przy użyciu usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="59684-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="59684-164">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="59684-165">Uwierzytelnianie wieloskładnikowe dla zarządzania systemem plików</span><span class="sxs-lookup"><span data-stu-id="59684-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="59684-166">Ta tooauthenticate za pomocą usługi Azure AD w celu wykonywania operacji (Tworzenie folderów, przekazywanie plików itp.).</span><span class="sxs-lookup"><span data-stu-id="59684-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="59684-167">Witaj następujący fragment kodu może być używany tooauthenticate aplikację przy użyciu usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="59684-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="59684-168">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59684-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="59684-169">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="59684-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="59684-170">Użyj powitania po toocreate fragment kodu grupy zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="59684-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="59684-171">Tworzenie klientów i konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="59684-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="59684-172">powitania po fragment najpierw tworzy hello usługi Data Lake Store konta klienta.</span><span class="sxs-lookup"><span data-stu-id="59684-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="59684-173">Używa powitania klienta obiektu toocreate konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="59684-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="59684-174">Na koniec fragment hello tworzy obiekt klient systemu plików.</span><span class="sxs-lookup"><span data-stu-id="59684-174">Finally, hello snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="59684-175">Wyświetlanie listy kont usługi Data Lake Store hello</span><span class="sxs-lookup"><span data-stu-id="59684-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="59684-176">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="59684-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="59684-177">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="59684-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="59684-178">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="59684-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="59684-179">Usuwanie katalogu</span><span class="sxs-lookup"><span data-stu-id="59684-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="59684-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="59684-180">See also</span></span>

- [<span data-ttu-id="59684-181">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="59684-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="59684-182">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="59684-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="59684-183">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="59684-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="59684-184">Dokumentacja zestawu SDK .NET usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="59684-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="59684-185">Dokumentacja interfejsu REST usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="59684-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
