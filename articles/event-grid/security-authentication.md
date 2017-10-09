---
title: "aaaAzure siatki zdarzeń zabezpieczeń i uwierzytelniania"
description: "Opisuje Azure zdarzeń siatki i jego pojęcia."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="19114-103">Zdarzenie siatki zabezpieczeń i uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="19114-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="19114-104">Azure siatki zdarzeń ma trzy typy uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="19114-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="19114-105">Subskrypcja zdarzeń</span><span class="sxs-lookup"><span data-stu-id="19114-105">Event subscriptions</span></span>
* <span data-ttu-id="19114-106">Publikowanie zdarzenia</span><span class="sxs-lookup"><span data-stu-id="19114-106">Event publishing</span></span>
* <span data-ttu-id="19114-107">Dostarczania zdarzeń elementu WebHook</span><span class="sxs-lookup"><span data-stu-id="19114-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="19114-108">Dostarczania zdarzeń elementu WebHook</span><span class="sxs-lookup"><span data-stu-id="19114-108">WebHook Event delivery</span></span>

<span data-ttu-id="19114-109">Element Webhook ma jeden wiele sposobów tooreceive zdarzeń w czasie rzeczywistym z siatki zdarzeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="19114-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="19114-110">Zawsze jest nowe zdarzenie toobe gotowy dostarczane, siatki zdarzeń wysyła żądanie HTTP z tooyour elementu WebHook ze zdarzeniem hello w treści hello.</span><span class="sxs-lookup"><span data-stu-id="19114-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="19114-111">Po zarejestrowaniu własny punkt końcowy elementu WebHook siatki zdarzeń wysyła możesz żądania POST z kodem poprawności w kolejności tooprove punktu końcowego własności.</span><span class="sxs-lookup"><span data-stu-id="19114-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="19114-112">Twoja aplikacja powinna toorespond przez wyświetlania kodu walidacji hello Wstecz.</span><span class="sxs-lookup"><span data-stu-id="19114-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="19114-113">Zdarzenie siatki nie wyśle zdarzenia tooWebHook punktów końcowych, które nie przeszły hello weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="19114-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="19114-114">Szczegóły dotyczące sprawdzania poprawności:</span><span class="sxs-lookup"><span data-stu-id="19114-114">Validation details:</span></span>

* <span data-ttu-id="19114-115">W czasie hello aktualizacja tworzenia subskrypcji zdarzeń siatki zdarzeń wpisów punktu końcowego "SubscriptionValidationEvent" zdarzeń toohello docelowej.</span><span class="sxs-lookup"><span data-stu-id="19114-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="19114-116">Zdarzenie Hello zawiera wartość nagłówka "Typ zdarzenia: Walidacja".</span><span class="sxs-lookup"><span data-stu-id="19114-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="19114-117">treści zdarzenia Hello ma hello tym samym schematem co inne zdarzenia, zdarzenia siatki.</span><span class="sxs-lookup"><span data-stu-id="19114-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="19114-118">Dane zdarzenia Hello zawiera właściwość "ValidationCode" z ciągiem losowo generowany np. "ValidationCode: acb13...".</span><span class="sxs-lookup"><span data-stu-id="19114-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="19114-119">W kolejności tooprove punktu końcowego własność, echo np. Kod weryfikacji wstecz hello "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="19114-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="19114-120">Na koniec jest toonote ważne, czy siatka zdarzeń Azure obsługuje tylko punktów końcowych HTTPS elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="19114-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="19114-121">Subskrypcja zdarzeń</span><span class="sxs-lookup"><span data-stu-id="19114-121">Event subscription</span></span>

<span data-ttu-id="19114-122">zdarzenia tooan toosubscribe, musi mieć hello **Microsoft.EventGrid/EventSubscriptions/Write** wymagane uprawnienie na powitania zasobów.</span><span class="sxs-lookup"><span data-stu-id="19114-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="19114-123">To uprawnienie jest konieczne, ponieważ pisania nową subskrypcję w zakresie hello hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="19114-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="19114-124">Witaj wymaganego zasobu różni się pod względem są subskrypcję tematu system tooa lub niestandardowego tematu.</span><span class="sxs-lookup"><span data-stu-id="19114-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="19114-125">Oba typy są opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="19114-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="19114-126">Tematy systemu (usługa Azure wydawców)</span><span class="sxs-lookup"><span data-stu-id="19114-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="19114-127">Tematy systemu należy toowrite uprawnienia nowej subskrypcji zdarzeń w zakresie hello publikowania zdarzeń hello hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="19114-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="19114-128">format Hello hello zasobu to:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="19114-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="19114-129">Na przykład toosubscribe tooan zdarzeń na konto magazynu o nazwie **myacct**, wymagane jest uprawnienie Microsoft.EventGrid/EventSubscriptions/Write hello na:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="19114-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="19114-130">Niestandardowe — tematy</span><span class="sxs-lookup"><span data-stu-id="19114-130">Custom topics</span></span>

<span data-ttu-id="19114-131">Tematy niestandardowe należy toowrite uprawnienia nowej subskrypcji zdarzeń w zakresie hello hello siatki zdarzenia tematu.</span><span class="sxs-lookup"><span data-stu-id="19114-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="19114-132">format Hello hello zasobu to:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="19114-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="19114-133">Na przykład toosubscribe tooa niestandardowego tematu o nazwie **mytopic**, wymagane jest uprawnienie Microsoft.EventGrid/EventSubscriptions/Write hello na:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="19114-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="19114-134">Publikowanie w temacie</span><span class="sxs-lookup"><span data-stu-id="19114-134">Topic publishing</span></span>

<span data-ttu-id="19114-135">Tematy za pomocą dostępu sygnatury dostępu Współdzielonego lub uwierzytelniania opartego na kluczu.</span><span class="sxs-lookup"><span data-stu-id="19114-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="19114-136">Firma Microsoft zaleca SAS, ale uwierzytelniania opartego na kluczu udostępnia prosty programowania i jest zgodny z wielu istniejących wydawców elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="19114-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="19114-137">Wartość uwierzytelniania hello objąć hello nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="19114-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="19114-138">Sygnatury dostępu Współdzielonego, można użyć **Æg sas token** hello wartości nagłówka.</span><span class="sxs-lookup"><span data-stu-id="19114-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="19114-139">Dla uwierzytelniania opartego na kluczu, użyj **Æg sas klucza** hello wartości nagłówka.</span><span class="sxs-lookup"><span data-stu-id="19114-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="19114-140">Uwierzytelnianie za pomocą klucza</span><span class="sxs-lookup"><span data-stu-id="19114-140">Key authentication</span></span>

<span data-ttu-id="19114-141">Uwierzytelnianie za pomocą klucza jest hello najprostszej formy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="19114-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="19114-142">Użyj formatu hello:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="19114-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="19114-143">Na przykład można przekazać klucza z:</span><span class="sxs-lookup"><span data-stu-id="19114-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="19114-144">Tokeny sygnatur dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="19114-144">SAS tokens</span></span>

<span data-ttu-id="19114-145">Tokeny sygnatury dostępu Współdzielonego dla zdarzeń siatki obejmują hello zasobu czas wygaśnięcia i podpis.</span><span class="sxs-lookup"><span data-stu-id="19114-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="19114-146">Witaj format tokenu sygnatury dostępu Współdzielonego hello jest: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="19114-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="19114-147">Hello zasób jest hello ścieżki dla toowhich tematu hello wysyłania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19114-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="19114-148">Na przykład ścieżka prawidłowego zasobu to:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="19114-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="19114-149">Podpis hello jest generowanie z klucza.</span><span class="sxs-lookup"><span data-stu-id="19114-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="19114-150">Na przykład prawidłowy **Æg sas token** wartość to:</span><span class="sxs-lookup"><span data-stu-id="19114-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="19114-151">Hello poniższy przykład tworzy token sygnatury dostępu Współdzielonego do użytku z siatki zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="19114-151">hello following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="19114-152">Kontrola dostępu administracyjnego</span><span class="sxs-lookup"><span data-stu-id="19114-152">Management Access Control</span></span>

<span data-ttu-id="19114-153">Azure siatki zdarzeń umożliwia możesz toocontrol hello poziom dostępu podany toodifferent użytkowników toodo różne operacje zarządzania, takie jak listy subskrypcji zdarzeń, tworzenie nowych i generowania kluczy.</span><span class="sxs-lookup"><span data-stu-id="19114-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="19114-154">Siatki zdarzenia dla tego korzysta z platformy Azure na podstawie ról dostępu Sprawdź (RBAC).</span><span class="sxs-lookup"><span data-stu-id="19114-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="19114-155">Typy operacji</span><span class="sxs-lookup"><span data-stu-id="19114-155">Operation types</span></span>

<span data-ttu-id="19114-156">Siatka zdarzeń platformy Azure obsługuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="19114-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="19114-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="19114-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="19114-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="19114-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="19114-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="19114-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="19114-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="19114-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="19114-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="19114-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="19114-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="19114-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="19114-163">Witaj ostatnie trzy operacje zwracany potencjalnie poufne informacje, które pobiera przefiltrowane z normalnych operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="19114-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="19114-164">Jest najlepszym rozwiązaniem dla Ciebie toorestrict dostępu toothese operacji.</span><span class="sxs-lookup"><span data-stu-id="19114-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="19114-165">Role niestandardowe można tworzyć przy użyciu [programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure interfejsu wiersza polecenia (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)i hello [interfejsu API REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="19114-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="19114-166">Wymuszanie roli na podstawie sprawdzanie dostępu (RBAC)</span><span class="sxs-lookup"><span data-stu-id="19114-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="19114-167">Użyj hello następujące kroki tooenforce RBAC dla różnych użytkowników:</span><span class="sxs-lookup"><span data-stu-id="19114-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="19114-168">Utwórz plik definicji niestandardowej roli zabezpieczeń (JSON)</span><span class="sxs-lookup"><span data-stu-id="19114-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="19114-169">Witaj poniżej przedstawiono przykładowe definicje ról siatki zdarzeń, których użytkownicy tooperform różnych zestawów działań.</span><span class="sxs-lookup"><span data-stu-id="19114-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="19114-170">**EventGridReadOnlyRole.json**: Zezwalaj tylko na tylko operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="19114-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="19114-171">**EventGridNoDeleteListKeysRole.json**: Zezwalaj na akcje po ograniczone, ale nie zezwalaj akcje usuwania.</span><span class="sxs-lookup"><span data-stu-id="19114-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="19114-172">**EventGridContributorRole.json**: umożliwia wszystkie akcje siatki zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19114-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="19114-173">Instalowanie i logowania tooAzure interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="19114-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="19114-174">Azure CLI w wersji 0.8.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="19114-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="19114-175">tooinstall hello najnowszej wersji i powiąż go z subskrypcją platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="19114-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="19114-176">Usługa Azure Resource Manager w interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="19114-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="19114-177">Przejdź za[hello Using Azure CLI z hello Resource Manager](../xplat-cli-azure-resource-manager.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="19114-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="19114-178">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="19114-178">Create a custom role</span></span>

<span data-ttu-id="19114-179">toocreate niestandardowej roli zabezpieczeń, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="19114-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="19114-180">Przypisz hello roli tooa użytkownika</span><span class="sxs-lookup"><span data-stu-id="19114-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="19114-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19114-181">Next steps</span></span>

* <span data-ttu-id="19114-182">Aby tooEvent wprowadzenie siatki, zobacz [o siatki zdarzeń](overview.md)</span><span class="sxs-lookup"><span data-stu-id="19114-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
