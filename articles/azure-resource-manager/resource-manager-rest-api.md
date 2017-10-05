---
title: "Interfejsy API REST usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Przegląd przykładów uwierzytelniania i użycia interfejsów API REST usługi Resource Manager"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="d3218-103">Interfejsy API REST Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="d3218-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3218-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3218-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="d3218-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d3218-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="d3218-106">Portal</span><span class="sxs-lookup"><span data-stu-id="d3218-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="d3218-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="d3218-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="d3218-108">Za każdego wywołania do usługi Azure Resource Manager za każdy wdrożonej szablon za każdego konta skonfigurowanego magazynu ma co najmniej jednego wywołania interfejsu API RESTful Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="d3218-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="d3218-109">Ten temat jest przeznaczony do tych interfejsów API i sposób ich wywołania bez przy użyciu dowolnego zestawu SDK w ogóle.</span><span class="sxs-lookup"><span data-stu-id="d3218-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="d3218-110">Ta metoda jest przydatna, jeśli mają pełną kontrolę nad żądań na platformie Azure lub jeśli zestaw SDK dla preferowany język jest niedostępny lub nie obsługuje operacji.</span><span class="sxs-lookup"><span data-stu-id="d3218-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="d3218-111">W tym artykule nie przechodzi przez każdy interfejs API, który jest narażony na platformie Azure, ale raczej używa niektóre operacje jako przykłady sposobu połączenia ich.</span><span class="sxs-lookup"><span data-stu-id="d3218-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="d3218-112">Po zrozumieniu podstaw możesz przeczytać [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) można znaleźć szczegółowe informacje na temat korzystania z resztą interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="d3218-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="d3218-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="d3218-113">Authentication</span></span>
<span data-ttu-id="d3218-114">Uwierzytelnianie dla Menedżera zasobów jest obsługiwane przez usługi Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="d3218-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="d3218-115">Aby połączyć się z jakiegokolwiek interfejsu API, należy najpierw uwierzytelniania za pomocą usługi Azure AD do tokenu uwierzytelniania, które można przekazać do każdego żądania odbierania.</span><span class="sxs-lookup"><span data-stu-id="d3218-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="d3218-116">Jak możemy zawierająca opis czysty wywołania bezpośrednio do interfejsów API REST przyjęto założenie, że nie chcesz uwierzytelniać przy wyświetlaniu monitu o nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="d3218-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="d3218-117">Możemy również założenie, że nie używasz dwa mechanizmy uwierzytelniania Multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="d3218-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="d3218-118">W związku z tym utworzymy tak zwany aplikacji usługi Azure AD i usługę podmiotu zabezpieczeń, które są używane podczas logowania się.</span><span class="sxs-lookup"><span data-stu-id="d3218-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="d3218-119">Należy jednak pamiętać, że usługi Azure AD obsługuje kilka procedur uwierzytelniania i wszystkich z nich można pobrać tokenu uwierzytelniania wymagane dla kolejnych żądań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d3218-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="d3218-120">Postępuj zgodnie z [Azure tworzenie aplikacji usługi AD i nazwę główną usługi](resource-group-create-service-principal-portal.md) instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="d3218-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="d3218-121">Generuje Token dostępu</span><span class="sxs-lookup"><span data-stu-id="d3218-121">Generating an Access Token</span></span>
<span data-ttu-id="d3218-122">Uwierzytelnianie w usłudze Azure AD odbywa się przez wywołanie do usługi Azure AD, znajdujący się w login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="d3218-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="d3218-123">Na potrzeby uwierzytelniania, musisz mieć następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="d3218-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="d3218-124">Identyfikator dzierżawy usługi Azure AD (nazwa tej usługi Azure AD są przy użyciu logowania, często taki sam, jak firma, ale nie jest konieczna)</span><span class="sxs-lookup"><span data-stu-id="d3218-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="d3218-125">Identyfikator aplikacji (podjętych podczas kroku tworzenia aplikacji usługi Azure AD)</span><span class="sxs-lookup"><span data-stu-id="d3218-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="d3218-126">Hasło (wybranej podczas tworzenia aplikacji usługi Azure AD)</span><span class="sxs-lookup"><span data-stu-id="d3218-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="d3218-127">W poniższych żądania HTTP upewnij się, że Zamień poprawne wartości "Identyfikator dzierżawy Azure AD", "Identyfikator aplikacji" i "Password".</span><span class="sxs-lookup"><span data-stu-id="d3218-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="d3218-128">**Rodzajowe żądanie HTTP:**</span><span class="sxs-lookup"><span data-stu-id="d3218-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="d3218-129">... zostanie (Jeśli uwierzytelnianie zakończy się powodzeniem) powoduje odpowiedź podobną do poniższej odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="d3218-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="d3218-130">(' Access_token ' w poprzedniej odpowiedzi zostały skrócone Aby zwiększyć czytelność)</span><span class="sxs-lookup"><span data-stu-id="d3218-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="d3218-131">**Generowanie tokenu dostępu, używając Bash:**</span><span class="sxs-lookup"><span data-stu-id="d3218-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="d3218-132">**Generowanie tokenu dostępu przy użyciu programu PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="d3218-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="d3218-133">Odpowiedź zawiera token dostępu, informacje o tym, jak długo token jest prawidłowy i informacje o jakie zasobów można użyć tokenu dla.</span><span class="sxs-lookup"><span data-stu-id="d3218-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="d3218-134">Token dostępu otrzymany w poprzedniego wywołania HTTP muszą być przekazywane w dla wszystkich żądań do interfejsu API Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="d3218-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="d3218-135">Przekaż go jako wartość nagłówka o nazwie "Autoryzacja" o wartości "Bearer YOUR_ACCESS_TOKEN".</span><span class="sxs-lookup"><span data-stu-id="d3218-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="d3218-136">Zwróć uwagę, odstęp między "Bearer" i tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d3218-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="d3218-137">Jak widać w powyższym wyników HTTP, token jest prawidłowy w danym okresie czasu, w którym powinien pamięci podręcznej i ponowne użycie tego samego tokenu.</span><span class="sxs-lookup"><span data-stu-id="d3218-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="d3218-138">Nawet jeśli jest możliwe do uwierzytelniania usługi Azure AD dla każdego wywołania interfejsu API, może być bardzo mało wydajne.</span><span class="sxs-lookup"><span data-stu-id="d3218-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="d3218-139">Menedżer zasobów wywołania interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="d3218-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="d3218-140">W tym temacie używa tylko kilka interfejsów API wyjaśnić podstawowe sposoby użycia operacji REST.</span><span class="sxs-lookup"><span data-stu-id="d3218-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="d3218-141">Aby uzyskać informacje o wszystkich operacji, zobacz [interfejsów API REST usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="d3218-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="d3218-142">Wyświetl listę wszystkich subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d3218-142">List all subscriptions</span></span>
<span data-ttu-id="d3218-143">Jednym z najprostszym operacje, które może wykonywać jest lista dostępnych subskrypcji, do których masz dostęp.</span><span class="sxs-lookup"><span data-stu-id="d3218-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="d3218-144">W poniższych zostanie wyświetlony, jak token dostępu jest przekazywany jako nagłówek:</span><span class="sxs-lookup"><span data-stu-id="d3218-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="d3218-145">(Zamiast YOUR_ACCESS_TOKEN Twojego rzeczywiste Token dostępu).</span><span class="sxs-lookup"><span data-stu-id="d3218-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="d3218-146">... i w związku z tym uzyskać listę subskrypcji, które może uzyskać dostępu do tej nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="d3218-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="d3218-147">(Identyfikatory subskrypcji zostały skrócone dla czytelności)</span><span class="sxs-lookup"><span data-stu-id="d3218-147">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="d3218-148">Wyświetl listę wszystkich grup zasobów w określonej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d3218-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="d3218-149">Wszystkie zasoby dostępne z interfejsów API Menedżera zasobów są zagnieżdżone w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d3218-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="d3218-150">Menedżer zasobów dla istniejącej grupy zasobów można badać w ramach subskrypcji, za pomocą następujących żądania HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="d3218-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="d3218-151">Zwróć uwagę, jak identyfikator subskrypcji jest przekazywany jako część adresu URL teraz.</span><span class="sxs-lookup"><span data-stu-id="d3218-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="d3218-152">(Zamiast YOUR_ACCESS_TOKEN i IDENTYFIKATOR_SUBSKRYPCJI dostępu rzeczywisty identyfikator token i subskrypcji)</span><span class="sxs-lookup"><span data-stu-id="d3218-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="d3218-153">Otrzymasz odpowiedź zależy od tego, czy zdefiniowano żadnych grup zasobów, a jeśli tak, jak wiele.</span><span class="sxs-lookup"><span data-stu-id="d3218-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="d3218-154">(Identyfikatory subskrypcji zostały skrócone dla czytelności)</span><span class="sxs-lookup"><span data-stu-id="d3218-154">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d3218-155">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d3218-155">Create a resource group</span></span>
<span data-ttu-id="d3218-156">Do tej pory firma Microsoft już tylko zostały zapytań interfejsów API Menedżera zasobów informacji.</span><span class="sxs-lookup"><span data-stu-id="d3218-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="d3218-157">Nadszedł czas, możemy utworzyć niektórych zasobów i Zacznijmy od Najprostszym z nich wszystkie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d3218-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="d3218-158">Następujące żądania HTTP tworzy grupę zasobów w regionu/lokalizacji, a następnie dodaje tag do niej.</span><span class="sxs-lookup"><span data-stu-id="d3218-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="d3218-159">(Zastąp YOUR_ACCESS_TOKEN, IDENTYFIKATOR_SUBSKRYPCJI, RESOURCE_GROUP_NAME z rzeczywistego tokenu dostępu, identyfikator subskrypcji i nazwę grupy zasobów, aby utworzyć)</span><span class="sxs-lookup"><span data-stu-id="d3218-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="d3218-160">W przypadku powodzenia można uzyskać odpowiedzi, która jest podobna do poniższej odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="d3218-160">If successful, you get a response that is similar to the following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="d3218-161">Pomyślnie utworzona grupa zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d3218-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="d3218-162">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="d3218-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="d3218-163">Wdrażanie zasobów w grupie zasobów, przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3218-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="d3218-164">Usługa Resource Manager można wdrożyć zasobów za pomocą szablonów.</span><span class="sxs-lookup"><span data-stu-id="d3218-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="d3218-165">Szablon definiuje kilka zasobów oraz ich zależności.</span><span class="sxs-lookup"><span data-stu-id="d3218-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="d3218-166">Dla tej sekcji przyjęto założenie, znasz szablony Menedżera zasobów i firma Microsoft tylko pokazano, jak wykonać wywołanie interfejsu API rozpocząć wdrażanie.</span><span class="sxs-lookup"><span data-stu-id="d3218-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="d3218-167">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d3218-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d3218-168">Wdrożenie szablonu nie różnią się znacznie sposób wywołania innych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="d3218-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="d3218-169">Jeden istotnym elementem jest, że wdrażania szablonu może zająć sporo czasu.</span><span class="sxs-lookup"><span data-stu-id="d3218-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="d3218-170">Po prostu zwraca wywołania interfejsu API i jest możesz jako Deweloper na zapytanie o stan wdrożenia, aby dowiedzieć się, gdy wdrożenie jest przeprowadzane.</span><span class="sxs-lookup"><span data-stu-id="d3218-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="d3218-171">Aby uzyskać więcej informacji, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d3218-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="d3218-172">W tym przykładzie używamy publicznie ujawnionych szablon dostępny na [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="d3218-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="d3218-173">Szablon, który używamy wdraża Maszynę wirtualną systemu Linux do regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="d3218-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="d3218-174">Mimo że w tym przykładzie używa szablonu dostępne w publicznych repozytorium, takich jak GitHub, zamiast tego można przekazać pełny szablon jako część żądania.</span><span class="sxs-lookup"><span data-stu-id="d3218-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="d3218-175">Należy pamiętać, że firma Microsoft wartości parametrów w żądaniu, które są używane w szablonie wdrożone.</span><span class="sxs-lookup"><span data-stu-id="d3218-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="d3218-176">(Zastąp IDENTYFIKATOR_SUBSKRYPCJI, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD i DNS_NAME_FOR_PUBLIC_IP wartości odpowiednich dla żądania)</span><span class="sxs-lookup"><span data-stu-id="d3218-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="d3218-177">Aby poprawić czytelność niniejszej dokumentacji została pominięta długich odpowiedzi JSON dla tego żądania.</span><span class="sxs-lookup"><span data-stu-id="d3218-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="d3218-178">Odpowiedź zawiera informacje dotyczące wdrażania opartego na szablonie, utworzony.</span><span class="sxs-lookup"><span data-stu-id="d3218-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3218-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3218-179">Next steps</span></span>

- <span data-ttu-id="d3218-180">Informacje na temat obsługi operacji asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d3218-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
