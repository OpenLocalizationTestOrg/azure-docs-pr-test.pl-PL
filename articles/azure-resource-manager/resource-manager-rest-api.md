---
title: "aaaResource Menedżera interfejsów API REST | Dokumentacja firmy Microsoft"
description: "Omówienie hello uwierzytelniania interfejsów API REST usługi Resource Manager i przykłady użycia"
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
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="9586e-103">Interfejsy API REST Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="9586e-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9586e-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9586e-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="9586e-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9586e-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="9586e-106">Portal</span><span class="sxs-lookup"><span data-stu-id="9586e-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="9586e-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="9586e-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="9586e-108">Za co wywołanie tooAzure Resource Manager za każdy wdrożonej szablon za co konto magazynu skonfigurowanych istnieją co najmniej jednego wywołania toohello usługi Azure Resource Manager przez interfejs API RESTful.</span><span class="sxs-lookup"><span data-stu-id="9586e-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="9586e-109">Ten temat jest przeznaczony toothose interfejsów API i sposób ich wywołania bez przy użyciu dowolnego zestawu SDK w ogóle.</span><span class="sxs-lookup"><span data-stu-id="9586e-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="9586e-110">Takie rozwiązanie jest przydatne, jeśli mają pełną kontrolę nad tooAzure żądania lub hello zestawu SDK dla preferowany język jest niedostępny lub nie obsługuje operacji hello, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="9586e-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="9586e-111">W tym artykule nie przechodzi przez każdy interfejs API, który jest narażony na platformie Azure, ale raczej używa niektóre operacje jako przykłady sposobu połączenia toothem.</span><span class="sxs-lookup"><span data-stu-id="9586e-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="9586e-112">Po zidentyfikowaniu podstawy hello może odczytywać hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind szczegółowe informacje dotyczące sposobu toouse hello reszty hello interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="9586e-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="9586e-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="9586e-113">Authentication</span></span>
<span data-ttu-id="9586e-114">Uwierzytelnianie dla Menedżera zasobów jest obsługiwane przez usługi Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="9586e-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="9586e-115">tooany tooconnect interfejsu API, musisz najpierw tooauthenticate z usługi Azure AD tooreceive tokenu uwierzytelniania, które można przekazać na żądanie tooevery.</span><span class="sxs-lookup"><span data-stu-id="9586e-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="9586e-116">Jak możemy są opisujące wywołanie czystej bezpośrednio toohello interfejsów API REST przyjęto założenie, że nie chcesz tooauthenticate przy wyświetlaniu monitu o nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="9586e-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="9586e-117">Możemy również założenie, że nie używasz dwa mechanizmy uwierzytelniania Multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="9586e-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="9586e-118">W związku z tym utworzymy tak zwany aplikacji usługi Azure AD i są używane toolog w nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="9586e-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="9586e-119">Należy jednak pamiętać, że usługi Azure AD obsługuje kilka procedur uwierzytelniania i wszystkich z nich może być używane tooretrieve ten token uwierzytelniania, czego potrzebujemy dla kolejnych żądań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9586e-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="9586e-120">Postępuj zgodnie z [Azure tworzenie aplikacji usługi AD i nazwę główną usługi](resource-group-create-service-principal-portal.md) instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="9586e-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="9586e-121">Generuje Token dostępu</span><span class="sxs-lookup"><span data-stu-id="9586e-121">Generating an Access Token</span></span>
<span data-ttu-id="9586e-122">Uwierzytelnianie w usłudze Azure AD odbywa się przez wywołanie metody limit tooAzure AD, znajdujący się w login.microsoftonline.com. tooauthenticate, należy hello toohave następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="9586e-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="9586e-123">Identyfikator dzierżawy usługi Azure AD (hello nazwa tej usługi Azure AD, czy używasz toolog w, często hello taki sam jak firmy, ale nie jest konieczna)</span><span class="sxs-lookup"><span data-stu-id="9586e-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="9586e-124">Identyfikator aplikacji (podjętych podczas kroku tworzenia aplikacji hello Azure AD)</span><span class="sxs-lookup"><span data-stu-id="9586e-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="9586e-125">Hasło (wybranej podczas tworzenia hello aplikacji usługi Azure AD)</span><span class="sxs-lookup"><span data-stu-id="9586e-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="9586e-126">Hello następujące żądania HTTP upewnij się, że tooreplace "Azure AD dzierżawy ID", "Identyfikator aplikacji" i "Password" hello poprawne wartości.</span><span class="sxs-lookup"><span data-stu-id="9586e-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="9586e-127">**Rodzajowe żądanie HTTP:**</span><span class="sxs-lookup"><span data-stu-id="9586e-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="9586e-128">... zostanie (Jeśli uwierzytelnianie zakończy się powodzeniem) powoduje odpowiedzi toohello podobne, po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="9586e-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

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
<span data-ttu-id="9586e-129">(' access_token ' hello w hello poprzedzających odpowiedzi zostały skrócone tooincrease czytelności)</span><span class="sxs-lookup"><span data-stu-id="9586e-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="9586e-130">**Generowanie tokenu dostępu, używając Bash:**</span><span class="sxs-lookup"><span data-stu-id="9586e-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="9586e-131">**Generowanie tokenu dostępu przy użyciu programu PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="9586e-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="9586e-132">odpowiedź Hello zawiera token dostępu, informacje o tym, jak długo token jest prawidłowy i informacje o jakie zasobów można użyć tokenu dla.</span><span class="sxs-lookup"><span data-stu-id="9586e-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="9586e-133">token dostępu Hello otrzymane w hello poprzedniego wywołania HTTP muszą być przekazywane w dla wszystkich toohello żądania interfejsu API Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="9586e-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="9586e-134">Przekaż go jako wartość nagłówka o nazwie "Autoryzacja" o wartości hello "Bearer YOUR_ACCESS_TOKEN".</span><span class="sxs-lookup"><span data-stu-id="9586e-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="9586e-135">Zwróć uwagę, hello odstęp między "Bearer" i tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9586e-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="9586e-136">Jak widać z hello powyżej wynik HTTP hello token jest prawidłowy dla określonego okresu czasu, w którym powinien pamięci podręcznej i ponowne użycie tego samego tokenu.</span><span class="sxs-lookup"><span data-stu-id="9586e-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="9586e-137">Nawet jeśli jest możliwe tooauthenticate w usłudze Azure AD dla każdego wywołania interfejsu API, może być bardzo mało wydajne.</span><span class="sxs-lookup"><span data-stu-id="9586e-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="9586e-138">Menedżer zasobów wywołania interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="9586e-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="9586e-139">W tym temacie używa tylko kilka interfejsów API tooexplain hello podstawowe sposoby użycia operacji REST hello.</span><span class="sxs-lookup"><span data-stu-id="9586e-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="9586e-140">Informacje o wszystkich operacji hello, zobacz [interfejsów API REST usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="9586e-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="9586e-141">Wyświetl listę wszystkich subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9586e-141">List all subscriptions</span></span>
<span data-ttu-id="9586e-142">Jednej z operacji najprostszym hello, które może wykonywać jest toolist hello dostępnych subskrypcji są dostępne.</span><span class="sxs-lookup"><span data-stu-id="9586e-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="9586e-143">Hello następujące żądania jest widoczny jak token dostępu hello jest przekazywany jako nagłówka:</span><span class="sxs-lookup"><span data-stu-id="9586e-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="9586e-144">(Zamiast YOUR_ACCESS_TOKEN Twojego rzeczywiste Token dostępu).</span><span class="sxs-lookup"><span data-stu-id="9586e-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="9586e-145">... i w związku z tym można uzyskać listę subskrypcji tej nazwy głównej usługi jest możliwość tooaccess</span><span class="sxs-lookup"><span data-stu-id="9586e-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="9586e-146">(Identyfikatory subskrypcji zostały skrócone dla czytelności)</span><span class="sxs-lookup"><span data-stu-id="9586e-146">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="9586e-147">Wyświetl listę wszystkich grup zasobów w określonej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9586e-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="9586e-148">Wszystkie zasoby dostępne z hello interfejsów API Menedżera zasobów są zagnieżdżone w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9586e-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="9586e-149">Menedżer zasobów dla istniejącej grupy zasobów można badać w ramach subskrypcji przy użyciu hello następujące żądania HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="9586e-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="9586e-150">Zwróć uwagę, jak identyfikator subskrypcji hello jest przekazywany jako część adresu URL hello teraz.</span><span class="sxs-lookup"><span data-stu-id="9586e-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="9586e-151">(Zamiast YOUR_ACCESS_TOKEN i IDENTYFIKATOR_SUBSKRYPCJI dostępu rzeczywisty identyfikator token i subskrypcji)</span><span class="sxs-lookup"><span data-stu-id="9586e-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="9586e-152">Witaj odpowiedzi, możesz uzyskać zależy od tego, czy zdefiniowano żadnych grup zasobów, a jeśli tak, jak wiele.</span><span class="sxs-lookup"><span data-stu-id="9586e-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="9586e-153">(Identyfikatory subskrypcji zostały skrócone dla czytelności)</span><span class="sxs-lookup"><span data-stu-id="9586e-153">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="9586e-154">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="9586e-154">Create a resource group</span></span>
<span data-ttu-id="9586e-155">Do tej pory firma Microsoft już tylko zostały zapytań hello interfejsów API Menedżera zasobów informacji.</span><span class="sxs-lookup"><span data-stu-id="9586e-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="9586e-156">Nadszedł czas, możemy utworzyć niektórych zasobów i Zacznijmy od hello Najprostszym z nich wszystkie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9586e-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="9586e-157">Hello następujące żądania HTTP tworzy grupę zasobów w regionu/lokalizacji i dodaje tooit tagu.</span><span class="sxs-lookup"><span data-stu-id="9586e-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="9586e-158">(Zastąp YOUR_ACCESS_TOKEN, IDENTYFIKATOR_SUBSKRYPCJI, RESOURCE_GROUP_NAME z rzeczywistego tokenu dostępu, identyfikator subskrypcji i nazwę grupy zasobów ma toocreate hello)</span><span class="sxs-lookup"><span data-stu-id="9586e-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

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

<span data-ttu-id="9586e-159">W przypadku powodzenia można uzyskać odpowiedzi, która jest podobne toohello po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="9586e-159">If successful, you get a response that is similar toohello following response:</span></span>

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

<span data-ttu-id="9586e-160">Pomyślnie utworzona grupa zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9586e-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="9586e-161">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="9586e-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="9586e-162">Wdrażanie grupy zasobów tooa zasobów przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9586e-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="9586e-163">Usługa Resource Manager można wdrożyć zasobów za pomocą szablonów.</span><span class="sxs-lookup"><span data-stu-id="9586e-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="9586e-164">Szablon definiuje kilka zasobów oraz ich zależności.</span><span class="sxs-lookup"><span data-stu-id="9586e-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="9586e-165">Dla tej sekcji przyjęto założenie, znasz szablony Menedżera zasobów i firma Microsoft tylko wyświetlić sposób toomake hello API wywołać toostart wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9586e-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="9586e-166">Aby uzyskać więcej informacji na temat tworzenia szablonów, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9586e-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9586e-167">Wdrożenie szablonu nie różnią się znacznie toohow wywołania innych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="9586e-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="9586e-168">Jeden istotnym elementem jest, że wdrażania szablonu może zająć sporo czasu.</span><span class="sxs-lookup"><span data-stu-id="9586e-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="9586e-169">Wywołanie interfejsu API Hello właśnie zwraca i jest tooyou jako tooquery developer stanu toofind wdrożenia hello wychodzących po zakończeniu wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="9586e-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="9586e-170">Aby uzyskać więcej informacji, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="9586e-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="9586e-171">W tym przykładzie używamy publicznie ujawnionych szablon dostępny na [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="9586e-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="9586e-172">Szablon Hello używamy wdraża regionu zachodnie stany USA toohello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9586e-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="9586e-173">Mimo że w tym przykładzie używa szablonu dostępne w publicznych repozytorium, takich jak GitHub, zamiast tego można przekazać hello pełny szablon jako część żądania hello.</span><span class="sxs-lookup"><span data-stu-id="9586e-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="9586e-174">Należy pamiętać, że firma Microsoft udostępnia wartości parametrów w żądaniu hello, które są używane wewnątrz hello wdrożyć szablon.</span><span class="sxs-lookup"><span data-stu-id="9586e-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="9586e-175">(Zastąp IDENTYFIKATOR_SUBSKRYPCJI, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD i DNS_NAME_FOR_PUBLIC_IP toovalues odpowiednie dla żądania)</span><span class="sxs-lookup"><span data-stu-id="9586e-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

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

<span data-ttu-id="9586e-176">Hello długi JSON odpowiedzi na to żądanie został pominięty tooimprove czytelność niniejszej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="9586e-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="9586e-177">odpowiedź Hello zawiera informacje o hello opartego na szablonie wdrożenia, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9586e-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9586e-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9586e-178">Next steps</span></span>

- <span data-ttu-id="9586e-179">toolearn dotyczące obsługi operacji asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="9586e-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
