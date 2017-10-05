---
title: "Zarządzanie Azure Data Lake Analytics przy użyciu języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć konto usługi Data Lake Store i przesyłać zadania za pomocą języka Python. "
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
ms.openlocfilehash: 31326a32f8748e6cfb8bfe24cda46c511ab59352
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="e71e0-103">Zarządzanie Azure Data Lake Analytics przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="e71e0-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="e71e0-104">Wersji języka Python</span><span class="sxs-lookup"><span data-stu-id="e71e0-104">Python versions</span></span>

* <span data-ttu-id="e71e0-105">Użyj 64-bitowej wersji języka Python.</span><span class="sxs-lookup"><span data-stu-id="e71e0-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="e71e0-106">Można użyć standardowego dystrybucję oprogramowania Python znaleźć pod adresem  **[pobiera Python.org](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="e71e0-106">You can use the standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="e71e0-107">Wielu deweloperów znaleźć łatwe w użyciu  **[dystrybucję oprogramowania Python Anaconda](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="e71e0-107">Many developers find it convenient to use the **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="e71e0-108">Ten artykuł dotyczy przy użyciu języka Python w wersji 3,6 z standardowe dystrybucję oprogramowania Python</span><span class="sxs-lookup"><span data-stu-id="e71e0-108">This article was written using Python version 3.6 from the standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="e71e0-109">Instalowanie zestawu Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="e71e0-109">Install Azure Python SDK</span></span>

<span data-ttu-id="e71e0-110">Instalowanie następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="e71e0-110">Install the following modules:</span></span>

* <span data-ttu-id="e71e0-111">**Zasobów azure-mgmt** moduł zawiera inne moduły Azure Active Directory itp.</span><span class="sxs-lookup"><span data-stu-id="e71e0-111">The **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="e71e0-112">**Azure-mgmt-datalake magazynu** moduł zawiera operacji zarządzania kontem usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e71e0-112">The **azure-mgmt-datalake-store** module includes the Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="e71e0-113">**Azure datalake magazynu** moduł zawiera operacje systemu plików usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e71e0-113">The **azure-datalake-store** module includes the Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="e71e0-114">**Usługi analiza danych azure** moduł zawiera operacje usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e71e0-114">The **azure-datalake-analytics** module includes the Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="e71e0-115">Najpierw upewnij się, masz najnowszą `pip` , uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e71e0-115">First, ensure you have the latest `pip` by running the following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="e71e0-116">Ten dokument został zapisany przy użyciu `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="e71e0-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="e71e0-117">Należy użyć następującego `pip` polecenia, aby zainstalować moduły w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="e71e0-117">Use the following `pip` commands to install the modules from the commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="e71e0-118">Utwórz nowy skrypt w języku Python</span><span class="sxs-lookup"><span data-stu-id="e71e0-118">Create a new Python script</span></span>

<span data-ttu-id="e71e0-119">Wklej następujący kod do skryptu:</span><span class="sxs-lookup"><span data-stu-id="e71e0-119">Paste the following code into the script:</span></span>

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

<span data-ttu-id="e71e0-120">Uruchom ten skrypt, aby zweryfikować, że można zaimportować moduły.</span><span class="sxs-lookup"><span data-stu-id="e71e0-120">Run this script to verify that the modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="e71e0-121">Authentication</span><span class="sxs-lookup"><span data-stu-id="e71e0-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="e71e0-122">Interakcyjnego uwierzytelniania użytkownika z okno podręczne</span><span class="sxs-lookup"><span data-stu-id="e71e0-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="e71e0-123">Ta metoda nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="e71e0-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="e71e0-124">Interakcyjnego uwierzytelniania użytkownika przy użyciu kodu urządzenia</span><span class="sxs-lookup"><span data-stu-id="e71e0-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter the user to authenticate with that has permission to subscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="e71e0-125">Uwierzytelnianie nieinteraktywne SPI i klucz tajny</span><span class="sxs-lookup"><span data-stu-id="e71e0-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="e71e0-126">Uwierzytelnianie nieinteraktywne za pomocą interfejsu API i certyfikatu</span><span class="sxs-lookup"><span data-stu-id="e71e0-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="e71e0-127">Ta metoda nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="e71e0-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="e71e0-128">Typowe zmienne skryptu</span><span class="sxs-lookup"><span data-stu-id="e71e0-128">Common script variables</span></span>

<span data-ttu-id="e71e0-129">Te zmienne są używane w przykładach.</span><span class="sxs-lookup"><span data-stu-id="e71e0-129">These variables are used in the samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-the-clients"></a><span data-ttu-id="e71e0-130">Utwórz klientów</span><span class="sxs-lookup"><span data-stu-id="e71e0-130">Create the clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="e71e0-131">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e71e0-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="e71e0-132">Tworzenie konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e71e0-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="e71e0-133">Najpierw utwórz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="e71e0-133">First create a store account.</span></span>

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
<span data-ttu-id="e71e0-134">Następnie utwórz konto ADLA, która używa tego magazynu.</span><span class="sxs-lookup"><span data-stu-id="e71e0-134">Then create an ADLA account that uses that store.</span></span>

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

## <a name="submit-a-job"></a><span data-ttu-id="e71e0-135">Prześlij zadanie</span><span class="sxs-lookup"><span data-stu-id="e71e0-135">Submit a job</span></span>

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
    TO "/data.csv"
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

## <a name="wait-for-a-job-to-end"></a><span data-ttu-id="e71e0-136">Poczekaj na zakończenie zadania</span><span class="sxs-lookup"><span data-stu-id="e71e0-136">Wait for a job to end</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="e71e0-137">Potoki listy i powtórzeń</span><span class="sxs-lookup"><span data-stu-id="e71e0-137">List pipelines and recurrences</span></span>
<span data-ttu-id="e71e0-138">W zależności od tego, czy Twoje zadania mają potoku lub ponownego metadanych dołączony, można wyświetlić listę potoki i powtórzeń.</span><span class="sxs-lookup"><span data-stu-id="e71e0-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="e71e0-139">Zarządzanie zasadami obliczeń</span><span class="sxs-lookup"><span data-stu-id="e71e0-139">Manage compute policies</span></span>

<span data-ttu-id="e71e0-140">Obiekt DataLakeAnalyticsAccountManagementClient zapewnia metody do zarządzania zasadami obliczeniowe dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e71e0-140">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="e71e0-141">Podać zasady obliczeń</span><span class="sxs-lookup"><span data-stu-id="e71e0-141">List compute policies</span></span>

<span data-ttu-id="e71e0-142">Poniższy kod pobiera listę zasad obliczeniowe dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e71e0-142">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="e71e0-143">Utwórz nowe zasady obliczeń</span><span class="sxs-lookup"><span data-stu-id="e71e0-143">Create a new compute policy</span></span>

<span data-ttu-id="e71e0-144">Poniższy kod tworzy nową zasadę obliczeniowe dla konta usługi Data Lake Analytics, ustawienie maksymalnej AUs, dostępne do określonego użytkownika do 50, a także priorytet zadania minimalna 250.</span><span class="sxs-lookup"><span data-stu-id="e71e0-144">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="e71e0-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e71e0-145">Next steps</span></span>

- <span data-ttu-id="e71e0-146">Aby wyświetlić ten samouczek przy użyciu innych narzędzi, kliknij odpowiedni selektor karty w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="e71e0-146">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
- <span data-ttu-id="e71e0-147">Aby dowiedzieć się więcej o języku U-SQL, zobacz [Wprowadzenie do języka U-SQL w usłudze Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e71e0-147">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="e71e0-148">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e71e0-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

