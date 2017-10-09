---
title: "aaaManage Azure Data Lake Analytics przy użyciu języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Python toocreate Data Lake przechowywać konta i przesyłanie zadań. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="9b655-103">Zarządzanie Azure Data Lake Analytics przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="9b655-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="9b655-104">Wersji języka Python</span><span class="sxs-lookup"><span data-stu-id="9b655-104">Python versions</span></span>

* <span data-ttu-id="9b655-105">Użyj 64-bitowej wersji języka Python.</span><span class="sxs-lookup"><span data-stu-id="9b655-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="9b655-106">Można użyć hello standardowe dystrybucję oprogramowania Python znaleźć pod adresem  **[pobiera Python.org](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="9b655-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="9b655-107">Wielu deweloperów znaleźć hello wygodne toouse  **[dystrybucję oprogramowania Python Anaconda](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="9b655-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="9b655-108">Ten artykuł dotyczy przy użyciu języka Python w wersji 3,6 z hello standardowe dystrybucję oprogramowania Python</span><span class="sxs-lookup"><span data-stu-id="9b655-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="9b655-109">Instalowanie zestawu Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="9b655-109">Install Azure Python SDK</span></span>

<span data-ttu-id="9b655-110">Zainstaluj hello następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="9b655-110">Install hello following modules:</span></span>

* <span data-ttu-id="9b655-111">Witaj **zasobów azure-mgmt** moduł zawiera inne moduły Azure Active Directory itp.</span><span class="sxs-lookup"><span data-stu-id="9b655-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="9b655-112">Witaj **azure-mgmt-datalake magazynu** moduł zawiera operacji zarządzania kontem usługi Azure Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="9b655-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="9b655-113">Witaj **azure datalake magazynu** moduł zawiera hello Azure Data Lake Store wykonywania operacji systemu plików.</span><span class="sxs-lookup"><span data-stu-id="9b655-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="9b655-114">Witaj **usługi analiza danych azure** moduł zawiera hello Azure Data Lake Analytics operacji.</span><span class="sxs-lookup"><span data-stu-id="9b655-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="9b655-115">Najpierw upewnij się, najnowsza wersja mają hello `pip` , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="9b655-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="9b655-116">Ten dokument został zapisany przy użyciu `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="9b655-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="9b655-117">Użyj następujących hello `pip` polecenia tooinstall modułów hello hello w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="9b655-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="9b655-118">Utwórz nowy skrypt w języku Python</span><span class="sxs-lookup"><span data-stu-id="9b655-118">Create a new Python script</span></span>

<span data-ttu-id="9b655-119">Wklej powitania po kodu do skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="9b655-119">Paste hello following code into hello script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="9b655-120">Uruchom ten skrypt tooverify tego hello, które mogą być importowane moduły.</span><span class="sxs-lookup"><span data-stu-id="9b655-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="9b655-121">Authentication</span><span class="sxs-lookup"><span data-stu-id="9b655-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="9b655-122">Interakcyjnego uwierzytelniania użytkownika z okno podręczne</span><span class="sxs-lookup"><span data-stu-id="9b655-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="9b655-123">Ta metoda nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="9b655-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="9b655-124">Interakcyjnego uwierzytelniania użytkownika przy użyciu kodu urządzenia</span><span class="sxs-lookup"><span data-stu-id="9b655-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="9b655-125">Uwierzytelnianie nieinteraktywne SPI i klucz tajny</span><span class="sxs-lookup"><span data-stu-id="9b655-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="9b655-126">Uwierzytelnianie nieinteraktywne za pomocą interfejsu API i certyfikatu</span><span class="sxs-lookup"><span data-stu-id="9b655-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="9b655-127">Ta metoda nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="9b655-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="9b655-128">Typowe zmienne skryptu</span><span class="sxs-lookup"><span data-stu-id="9b655-128">Common script variables</span></span>

<span data-ttu-id="9b655-129">Te zmienne są używane w hello próbek.</span><span class="sxs-lookup"><span data-stu-id="9b655-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="9b655-130">Utwórz klientom Witaj</span><span class="sxs-lookup"><span data-stu-id="9b655-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="9b655-131">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9b655-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="9b655-132">Tworzenie konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9b655-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="9b655-133">Najpierw utwórz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="9b655-133">First create a store account.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
<span data-ttu-id="9b655-134">Następnie utwórz konto ADLA, która używa tego magazynu.</span><span class="sxs-lookup"><span data-stu-id="9b655-134">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="9b655-135">Prześlij zadanie</span><span class="sxs-lookup"><span data-stu-id="9b655-135">Submit a job</span></span>

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="9b655-136">Poczekaj, aż tooend zadania</span><span class="sxs-lookup"><span data-stu-id="9b655-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="9b655-137">Potoki listy i powtórzeń</span><span class="sxs-lookup"><span data-stu-id="9b655-137">List pipelines and recurrences</span></span>
<span data-ttu-id="9b655-138">W zależności od tego, czy Twoje zadania mają potoku lub ponownego metadanych dołączony, można wyświetlić listę potoki i powtórzeń.</span><span class="sxs-lookup"><span data-stu-id="9b655-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="9b655-139">Zarządzanie zasadami obliczeń</span><span class="sxs-lookup"><span data-stu-id="9b655-139">Manage compute policies</span></span>

<span data-ttu-id="9b655-140">Obiekt DataLakeAnalyticsAccountManagementClient Hello zapewnia metody do zarządzania hello obliczeniowe zasady dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9b655-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="9b655-141">Podać zasady obliczeń</span><span class="sxs-lookup"><span data-stu-id="9b655-141">List compute policies</span></span>

<span data-ttu-id="9b655-142">powitania po kod pobiera listę zasad obliczeniowe dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9b655-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="9b655-143">Utwórz nowe zasady obliczeń</span><span class="sxs-lookup"><span data-stu-id="9b655-143">Create a new compute policy</span></span>

<span data-ttu-id="9b655-144">powitania po kod tworzy nową zasadę obliczeniowe dla konta usługi Data Lake Analytics, ustawienie hello maksymalną AUs dostępne toohello określonego użytkownika too50 i too250 priorytet zadania minimalna hello.</span><span class="sxs-lookup"><span data-stu-id="9b655-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="9b655-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b655-145">Next steps</span></span>

- <span data-ttu-id="9b655-146">toosee hello sam samouczek przy użyciu innych narzędzi, kliknij przycisk hello selektor karty w górnej części hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="9b655-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="9b655-147">toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9b655-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="9b655-148">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9b655-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

