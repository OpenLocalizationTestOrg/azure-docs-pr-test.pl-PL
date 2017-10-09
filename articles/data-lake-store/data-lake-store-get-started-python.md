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
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu języka Python

> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Zestaw SDK platformy .NET](data-lake-store-get-started-net-sdk.md)
> * [Zestaw SDK Java](data-lake-store-get-started-java-sdk.md)
> * [Interfejs API REST](data-lake-store-get-started-rest-api.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Dowiedz się jak toouse hello zestaw SDK Python platformy Azure i usługi Azure Data Lake Store tooperform podstawowe operacje takie jak tworzenie folderów, przekazywanie i pobieranie plików danych itp. Aby uzyskać więcej informacji o usłudze Data Lake, zobacz temat [Usługa Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne

* **Python**. Możesz pobrać środowisko Python [tutaj](https://www.python.org/downloads/). W tym artykule używany jest język Python 3.5.2.

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Utworzenie aplikacji usługi Azure Active Directory**. Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Store aplikacji z usługą Azure AD. Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**. Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Instalowanie modułów hello

toowork z Data Lake Store z użyciem języka Python, należy tooinstall trzech modułów.

* Witaj `azure-mgmt-resource` modułu. Obejmuje to moduły platformy Azure dla usługi Active Directory itp.
* Witaj `azure-mgmt-datalake-store` modułu. W tym operacji zarządzania kontem usługi Azure Data Lake Store hello. Aby uzyskać więcej informacji na temat tego modułu, zobacz [dokumentację modułu do zarządzania dla usługi Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).
* Witaj `azure-datalake-store` modułu. W tym hello Azure Data Lake Store wykonywania operacji systemu plików. Aby uzyskać więcej informacji na temat tego modułu, zobacz [dokumentację modułu systemu plików dla usługi Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).

Użyj następujących hello polecenia tooinstall hello modułów.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Tworzenie nowej aplikacji w języku Python

1. W hello IDE wyboru Utwórz nową aplikację języka Python, na przykład **mysample.py**.

2. Dodaj następujące wiersze tooimport hello wymagane moduły hello

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

3. Zapisz zmiany toomysample.py.

## <a name="authentication"></a>Authentication

W tej sekcji są omawiane tooauthenticate różne sposoby hello z usługą Azure AD. dostępne opcje Hello to:

* Uwierzytelnianie użytkowników końcowych
* Uwierzytelnianie między usługami
* Uwierzytelnianie wieloskładnikowe

Te opcje uwierzytelnianie muszą być używane dla modułów zarządzania kontami i zarządzania systemem plików.

### <a name="end-user-authentication-for-account-management"></a>Uwierzytelnianie użytkowników końcowych w celu zarządzania kontami

Ta tooauthenticate za pomocą usługi Azure AD dla operacji zarządzania kontem (Tworzenie/usuwanie konta usługi Data Lake Store itp.). Należy podać nazwę i hasło użytkownika usługi Azure AD. Należy pamiętać, że użytkownik hello nie powinno być skonfigurowane dla usługi Multi-Factor authentication.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Uwierzytelnianie użytkowników końcowych dla operacji systemu plików

Ta tooauthenticate za pomocą usługi Azure AD w celu wykonywania operacji (Tworzenie folderów, przekazywanie plików itp.). Użyj tej metody wraz z istniejącą natywną aplikacją **kliencką** usługi Azure AD. Podaj poświadczenia dla użytkownika Hello Azure AD nie powinno być skonfigurowane dla usługi Multi-Factor authentication.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>Uwierzytelnianie między usługami z kluczem tajnym klienta w celu zarządzania kontami

Ta tooauthenticate za pomocą usługi Azure AD dla operacji zarządzania kontem (Tworzenie/usuwanie konta usługi Data Lake Store itp.). Witaj następujący fragment kodu mogą być używane tooauthenticate aplikacji nieinteraktywnie, przy użyciu klucza tajnego powitania klienta dla aplikacji / usługi podmiotu zabezpieczeń. Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Uwierzytelnianie między usługami z wpisem tajnym klienta dla operacji systemu plików

Ta tooauthenticate za pomocą usługi Azure AD w celu wykonywania operacji (Tworzenie folderów, przekazywanie plików itp.). Witaj następujący fragment kodu mogą być używane tooauthenticate aplikacji nieinteraktywnie, przy użyciu klucza tajnego powitania klienta dla aplikacji / usługi podmiotu zabezpieczeń. Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Uwierzytelnianie wieloskładnikowe w celu zarządzania kontami

Ta tooauthenticate za pomocą usługi Azure AD dla operacji zarządzania kontem (Tworzenie/usuwanie konta usługi Data Lake Store itp.). Witaj następujący fragment kodu może być używany tooauthenticate aplikację przy użyciu usługi Multi-Factor authentication. Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.

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

### <a name="multi-factor-authentication-for-filesystem-management"></a>Uwierzytelnianie wieloskładnikowe dla zarządzania systemem plików

Ta tooauthenticate za pomocą usługi Azure AD w celu wykonywania operacji (Tworzenie folderów, przekazywanie plików itp.). Witaj następujący fragment kodu może być używany tooauthenticate aplikację przy użyciu usługi Multi-Factor authentication. Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Tworzenie grupy zasobów platformy Azure

Użyj powitania po toocreate fragment kodu grupy zasobów platformy Azure:

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

## <a name="create-clients-and-data-lake-store-account"></a>Tworzenie klientów i konta usługi Data Lake Store

powitania po fragment najpierw tworzy hello usługi Data Lake Store konta klienta. Używa powitania klienta obiektu toocreate konto usługi Data Lake Store. Na koniec fragment hello tworzy obiekt klient systemu plików.

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

## <a name="list-hello-data-lake-store-accounts"></a>Wyświetlanie listy kont usługi Data Lake Store hello

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Tworzenie katalogu

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Przekazywanie pliku


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Pobieranie pliku

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Usuwanie katalogu

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Zobacz też

- [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
- [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Dokumentacja zestawu SDK .NET usługi Data Lake Store](https://msdn.microsoft.com/library/mt581387.aspx)
- [Dokumentacja interfejsu REST usługi Data Lake Store](https://msdn.microsoft.com/library/mt693424.aspx)
