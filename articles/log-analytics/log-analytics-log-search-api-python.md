---
title: "aaaPython skryptu tooretrieve dane z usługi Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Interfejs API dziennika analizy dziennika wyszukiwania Hello umożliwia dowolnego klienta interfejsu API REST tooretrieve danych z obszaru roboczego analizy dzienników.  Ten artykuł zawiera przykładowy skrypt języka Python za pomocą hello interfejs API dziennika wyszukiwania."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: bwren
ms.openlocfilehash: a45693b04cd388301b859e7186ca671786d0229e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrieve-data-from-log-analytics-with-a-python-script"></a><span data-ttu-id="a9e54-104">Pobieranie danych z analizy dzienników przy użyciu skryptu języka Python</span><span class="sxs-lookup"><span data-stu-id="a9e54-104">Retrieve data from Log Analytics with a Python script</span></span>
<span data-ttu-id="a9e54-105">Witaj [interfejs API dziennika analizy dziennika wyszukiwania](log-analytics-log-search-api.md) umożliwia dowolnego klienta interfejsu API REST tooretrieve danych z obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="a9e54-105">hello [Log Analytics Log Search API](log-analytics-log-search-api.md) allows any REST API client tooretrieve data from a Log Analytics workspace.</span></span>  <span data-ttu-id="a9e54-106">W tym artykule przedstawiono przykładowy skrypt języka Python, używającej hello interfejs API dziennika analizy dziennika wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a9e54-106">This article presents a sample Python script that uses hello Log Analytics Log Search API.</span></span>  

## <a name="authentication"></a><span data-ttu-id="a9e54-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="a9e54-107">Authentication</span></span>
<span data-ttu-id="a9e54-108">Ten skrypt używa nazwy głównej usługi w usłudze Azure Active Directory tooauthenticate toohello w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="a9e54-108">This script uses a service principal in Azure Active Directory tooauthenticate toohello workspace.</span></span>  <span data-ttu-id="a9e54-109">Zezwalaj na nazwy główne usług klienta toorequest aplikacji, która hello usługi uwierzytelniania konta, nawet jeśli powitania klienta nie ma nazwy konta hello.</span><span class="sxs-lookup"><span data-stu-id="a9e54-109">Service principals allow a client application toorequest that hello service authenticate an account even if hello client does not have hello account name.</span></span> <span data-ttu-id="a9e54-110">Przed wykonaniem tego skryptu, należy utworzyć przy użyciu procesu hello na nazwy głównej usługi [aplikacji usługi Azure Active Directory i nazwy głównej usługi, który ma dostęp do zasobów, użyj portalu toocreate](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a9e54-110">Before running this script, you must create a service principal using hello process at [Use portal toocreate an Azure Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>  <span data-ttu-id="a9e54-111">Będziesz potrzebować tooprovide hello identyfikator aplikacji, identyfikator dzierżawy i klucz uwierzytelniania toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="a9e54-111">You'll need tooprovide hello Application ID, Tenant ID, and Authentication Key toohello script.</span></span> 

> [!NOTE]
> <span data-ttu-id="a9e54-112">Gdy użytkownik [utworzyć konto usługi Automatyzacja Azure](../automation/automation-create-standalone-account.md), nazwy głównej usługi jest tworzony czyli odpowiedniego toouse za pomocą tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="a9e54-112">When you [create an Azure Automation account](../automation/automation-create-standalone-account.md), a service principal is created that is suitable toouse with this script.</span></span>  <span data-ttu-id="a9e54-113">Jeśli masz już nazwy głównej usługi utworzonych przez usługi Automatyzacja Azure, powinno być możliwe toouse go zamiast tworzenia nowej, chociaż może być konieczne zbyt[utworzyć klucz uwierzytelniania](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) Jeśli go nie ma jeszcze.</span><span class="sxs-lookup"><span data-stu-id="a9e54-113">If you already have a service principal created by Azure Automation then you should be able toouse it instead of creating a new one, although you may need too[create an authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) if it doesn't already have one.</span></span>

## <a name="script"></a><span data-ttu-id="a9e54-114">Skrypt</span><span class="sxs-lookup"><span data-stu-id="a9e54-114">Script</span></span>
``` python
import adal
import requests
import json
import datetime
from pprint import pprint

# Details of workspace.  Fill in details for your workspace.
resource_group = 'xxxxxxxx'
workspace = 'xxxxxxxx'

# Details of query.  Modify these tooyour requirements.
query = "Type=Event"
end_time = datetime.datetime.utcnow()
start_time = end_time - datetime.timedelta(hours=24)
num_results = 100  # If not provided, a default of 10 results will be used.

# IDs for authentication.  Fill in values for your service principal.
subscription_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
tenant_id = 'xxxxxxxx-xxxx-xxxx-xxx-xxxxxxxxxxxx'
application_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx'
application_key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

# URLs for authentication
authentication_endpoint = 'https://login.microsoftonline.com/'
resource  = 'https://management.core.windows.net/'

# Get access token
context = adal.AuthenticationContext('https://login.microsoftonline.com/' + tenant_id)
token_response = context.acquire_token_with_client_credentials('https://management.core.windows.net/', application_id, application_key)
access_token = token_response.get('accessToken')

# Add token tooheader
headers = {
    "Authorization": 'Bearer ' + access_token,
    "Content-Type":'application/json'
}

# URLs for retrieving data
uri_base = 'https://management.azure.com'
uri_api = 'api-version=2015-11-01-preview'
uri_subscription = 'https://management.azure.com/subscriptions/' + subscription_id
uri_resourcegroup = uri_subscription + '/resourcegroups/'+ resource_group
uri_workspace = uri_resourcegroup + '/providers/Microsoft.OperationalInsights/workspaces/' + workspace
uri_search = uri_workspace + '/search'

# Build search parameters from query details
search_params = {
        "query": query,
        "top": num_results,
        "start": start_time.strftime('%Y-%m-%dT%H:%M:%S'),
        "end": end_time.strftime('%Y-%m-%dT%H:%M:%S')
        }

# Build URL and send post request
uri = uri_search + '?' + uri_api
response = requests.post(uri,json=search_params,headers=headers)

# Response of 200 if successful
if response.status_code == 200:

    # Parse hello response tooget hello ID and status
    data = response.json()
    search_id = data["id"].split("/")
    id = search_id[len(search_id)-1]
    status = data["__metadata"]["Status"]

    # If status is pending, then keep checking until complete
    while status == "Pending":

        # Build URL tooget search from ID and send request
        uri_search = uri_search + '/' + id
        uri = uri_search + '?' + uri_api
        response = requests.get(uri,headers=headers)

        # Parse hello response tooget hello status
        data = response.json()
        status = data["__metadata"]["Status"]

else:

    # Request failed
    print (response.status_code)
    response.raise_for_status()

print ("Total records:" + str(data["__metadata"]["total"]))
print ("Returned top:" + str(data["__metadata"]["top"]))
pprint (data["value"])
```
## <a name="next-steps"></a><span data-ttu-id="a9e54-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9e54-115">Next steps</span></span>
- <span data-ttu-id="a9e54-116">Dowiedz się więcej o hello [interfejs API dziennika analizy dziennika wyszukiwania](log-analytics-log-search-api.md).</span><span class="sxs-lookup"><span data-stu-id="a9e54-116">Learn more about hello [Log Analytics Log Search API](log-analytics-log-search-api.md).</span></span>
