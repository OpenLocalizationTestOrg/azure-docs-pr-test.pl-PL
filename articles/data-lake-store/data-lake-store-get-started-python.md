---
title: "Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu zestawu SDK języka Python | Microsoft Docs"
description: "Dowiedz się, jak używać zestawu SDK języka Python do pracy z kontami usługi Data Lake Store i systemem plików."
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
ms.openlocfilehash: 375a603360ac249fc1b08923a94c85652390a3fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="a4640-103">Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="a4640-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4640-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a4640-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="a4640-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4640-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="a4640-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="a4640-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="a4640-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="a4640-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="a4640-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="a4640-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="a4640-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a4640-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="a4640-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="a4640-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="a4640-111">Python</span><span class="sxs-lookup"><span data-stu-id="a4640-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="a4640-112">Dowiedz się, jak używać zestawu SDK języka Python dla usługi Azure Data Lake Store, aby wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych itp. Aby uzyskać więcej informacji o usłudze Data Lake, zobacz temat [Usługa Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4640-112">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4640-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a4640-113">Prerequisites</span></span>

* <span data-ttu-id="a4640-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="a4640-114">**Python**.</span></span> <span data-ttu-id="a4640-115">Możesz pobrać środowisko Python [tutaj](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a4640-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="a4640-116">W tym artykule używany jest język Python 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="a4640-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="a4640-117">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="a4640-117">**An Azure subscription**.</span></span> <span data-ttu-id="a4640-118">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4640-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a4640-119">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4640-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="a4640-120">Za pomocą aplikacji usługi Azure AD można uwierzytelnić aplikację usługi Data Lake Store w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="a4640-121">Istnieją różne metody uwierzytelniania w usłudze Azure AD: **uwierzytelnianie użytkowników końcowych** i **uwierzytelnianie między usługami**.</span><span class="sxs-lookup"><span data-stu-id="a4640-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a4640-122">Aby uzyskać instrukcje i więcej informacji na temat uwierzytelniania, zobacz [Uwierzytelnianie użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [Uwierzytelnianie między usługami](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a4640-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="a4640-123">Instalacja modułów</span><span class="sxs-lookup"><span data-stu-id="a4640-123">Install the modules</span></span>

<span data-ttu-id="a4640-124">Aby móc pracować z usługą Data Lake Store przy użyciu języka Python, musisz zainstalować trzy moduły.</span><span class="sxs-lookup"><span data-stu-id="a4640-124">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="a4640-125">Moduł `azure-mgmt-resource`.</span><span class="sxs-lookup"><span data-stu-id="a4640-125">The `azure-mgmt-resource` module.</span></span> <span data-ttu-id="a4640-126">Obejmuje to moduły platformy Azure dla usługi Active Directory itp.</span><span class="sxs-lookup"><span data-stu-id="a4640-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="a4640-127">Moduł `azure-mgmt-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="a4640-127">The `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="a4640-128">Obejmuje to operacje zarządzania kontem usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a4640-128">This includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="a4640-129">Aby uzyskać więcej informacji na temat tego modułu, zobacz [dokumentację modułu do zarządzania dla usługi Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="a4640-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="a4640-130">Moduł `azure-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="a4640-130">The `azure-datalake-store` module.</span></span> <span data-ttu-id="a4640-131">Obejmuje to operacje na systemie plików usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a4640-131">This includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="a4640-132">Aby uzyskać więcej informacji na temat tego modułu, zobacz [dokumentację modułu systemu plików dla usługi Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="a4640-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="a4640-133">Użyj następujących poleceń, aby zainstalować moduły.</span><span class="sxs-lookup"><span data-stu-id="a4640-133">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="a4640-134">Tworzenie nowej aplikacji w języku Python</span><span class="sxs-lookup"><span data-stu-id="a4640-134">Create a new Python application</span></span>

1. <span data-ttu-id="a4640-135">W wybranym środowisku IDE utwórz nową aplikację w języku Python, na przykład **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="a4640-135">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="a4640-136">Dodaj następujące wiersze, aby zaimportować wymagane moduły</span><span class="sxs-lookup"><span data-stu-id="a4640-136">Add the following lines to import the required modules</span></span>

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

3. <span data-ttu-id="a4640-137">Zapisz zmiany w aplikacji mysample.py.</span><span class="sxs-lookup"><span data-stu-id="a4640-137">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="a4640-138">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="a4640-138">Authentication</span></span>

<span data-ttu-id="a4640-139">W tej sekcji omówione zostaną różne sposoby uwierzytelniania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-139">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="a4640-140">Dostępne opcje:</span><span class="sxs-lookup"><span data-stu-id="a4640-140">The options available are:</span></span>

* <span data-ttu-id="a4640-141">Uwierzytelnianie użytkowników końcowych</span><span class="sxs-lookup"><span data-stu-id="a4640-141">End-user authentication</span></span>
* <span data-ttu-id="a4640-142">Uwierzytelnianie między usługami</span><span class="sxs-lookup"><span data-stu-id="a4640-142">Service-to-service authentication</span></span>
* <span data-ttu-id="a4640-143">Uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="a4640-143">Multi-factor authentication</span></span>

<span data-ttu-id="a4640-144">Te opcje uwierzytelnianie muszą być używane dla modułów zarządzania kontami i zarządzania systemem plików.</span><span class="sxs-lookup"><span data-stu-id="a4640-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="a4640-145">Uwierzytelnianie użytkowników końcowych w celu zarządzania kontami</span><span class="sxs-lookup"><span data-stu-id="a4640-145">End-user authentication for account management</span></span>

<span data-ttu-id="a4640-146">Użyj tej metody, aby uwierzytelnić się za pomocą usługi Azure AD w celu wykonywania operacji zarządzania kontem (tworzenie/usuwanie konta usługi Data Lake Store itp.).</span><span class="sxs-lookup"><span data-stu-id="a4640-146">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="a4640-147">Należy podać nazwę i hasło użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="a4640-148">Należy pamiętać, że użytkownik nie powinien być skonfigurowany do uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="a4640-148">Note that the user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="a4640-149">Uwierzytelnianie użytkowników końcowych dla operacji systemu plików</span><span class="sxs-lookup"><span data-stu-id="a4640-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="a4640-150">Użyj tej metody, aby uwierzytelniać przy użyciu usługi Azure AD w przypadku operacji systemu plików (tworzenie folderu, przekazywanie pliku itp.).</span><span class="sxs-lookup"><span data-stu-id="a4640-150">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="a4640-151">Użyj tej metody wraz z istniejącą natywną aplikacją **kliencką** usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="a4640-152">Użytkownik usługi Azure AD, dla którego podajesz poświadczenia, nie powinien być skonfigurowany do uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="a4640-152">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="a4640-153">Uwierzytelnianie między usługami z kluczem tajnym klienta w celu zarządzania kontami</span><span class="sxs-lookup"><span data-stu-id="a4640-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="a4640-154">Użyj tej metody, aby uwierzytelnić się za pomocą usługi Azure AD w celu wykonywania operacji zarządzania kontem (tworzenie/usuwanie konta usługi Data Lake Store itp.).</span><span class="sxs-lookup"><span data-stu-id="a4640-154">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="a4640-155">Poniższego fragmentu kodu można użyć do uwierzytelniania aplikacji w sposób nieinterakcyjny za pomocą klucza tajnego klienta aplikacji / nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="a4640-155">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="a4640-156">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="a4640-157">Uwierzytelnianie między usługami z wpisem tajnym klienta dla operacji systemu plików</span><span class="sxs-lookup"><span data-stu-id="a4640-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="a4640-158">Użyj tej metody, aby uwierzytelniać przy użyciu usługi Azure AD w przypadku operacji systemu plików (tworzenie folderu, przekazywanie pliku itp.).</span><span class="sxs-lookup"><span data-stu-id="a4640-158">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="a4640-159">Poniższego fragmentu kodu można użyć do uwierzytelniania aplikacji w sposób nieinterakcyjny za pomocą klucza tajnego klienta aplikacji / nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="a4640-159">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="a4640-160">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="a4640-161">Uwierzytelnianie wieloskładnikowe w celu zarządzania kontami</span><span class="sxs-lookup"><span data-stu-id="a4640-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="a4640-162">Użyj tej metody, aby uwierzytelnić się za pomocą usługi Azure AD w celu wykonywania operacji zarządzania kontem (tworzenie/usuwanie konta usługi Data Lake Store itp.).</span><span class="sxs-lookup"><span data-stu-id="a4640-162">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="a4640-163">Poniższego fragmentu kodu można użyć do uwierzytelniania aplikacji za pomocą uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="a4640-163">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="a4640-164">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="a4640-165">Uwierzytelnianie wieloskładnikowe dla zarządzania systemem plików</span><span class="sxs-lookup"><span data-stu-id="a4640-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="a4640-166">Użyj tej metody, aby uwierzytelniać przy użyciu usługi Azure AD w przypadku operacji systemu plików (tworzenie folderu, przekazywanie pliku itp.).</span><span class="sxs-lookup"><span data-stu-id="a4640-166">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="a4640-167">Poniższego fragmentu kodu można użyć do uwierzytelniania aplikacji za pomocą uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="a4640-167">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="a4640-168">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4640-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="a4640-169">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a4640-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="a4640-170">Aby utworzyć grupę zasobów platformy Azure, użyj poniższego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="a4640-170">Use the following code snippet to create an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="a4640-171">Tworzenie klientów i konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a4640-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="a4640-172">Poniższy fragment kodu najpierw tworzy klienta konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a4640-172">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="a4640-173">Używa on obiektu klienta do utworzenia konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a4640-173">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="a4640-174">Na koniec fragment kodu tworzy obiekt klienta systemu plików.</span><span class="sxs-lookup"><span data-stu-id="a4640-174">Finally, the snippet creates a filesystem client object.</span></span>

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

## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="a4640-175">Wyświetlanie listy kont usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a4640-175">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="a4640-176">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="a4640-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="a4640-177">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="a4640-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="a4640-178">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="a4640-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="a4640-179">Usuwanie katalogu</span><span class="sxs-lookup"><span data-stu-id="a4640-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="a4640-180">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a4640-180">See also</span></span>

- [<span data-ttu-id="a4640-181">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a4640-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="a4640-182">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a4640-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="a4640-183">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a4640-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="a4640-184">Dokumentacja zestawu SDK .NET usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a4640-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="a4640-185">Dokumentacja interfejsu REST usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a4640-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
