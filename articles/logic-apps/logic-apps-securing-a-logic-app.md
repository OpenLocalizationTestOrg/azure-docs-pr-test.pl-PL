---
title: "aaaSecure dostęp do aplikacji logiki tooAzure | Dokumentacja firmy Microsoft"
description: "Dodawanie zabezpieczeń do ochrony tootriggers dostępu, danych wejściowych i wyjściowych parametry akcji i usług używanych wraz z przepływów pracy w programie Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="c5314-103">Bezpieczny dostęp do aplikacji logiki tooyour</span><span class="sxs-lookup"><span data-stu-id="c5314-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="c5314-104">Istnieje wiele toohelp dostępne narzędzia, które należy zabezpieczyć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="c5314-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="c5314-105">Zabezpieczanie dostępu tootrigger aplikacja logiki (wyzwalacza żądania HTTP)</span><span class="sxs-lookup"><span data-stu-id="c5314-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="c5314-106">Zabezpieczanie dostępu toomanage, edytować lub odczytać aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="c5314-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="c5314-107">Zabezpieczanie dostępu toocontents z wejściami i wyjściami dla przebiegu</span><span class="sxs-lookup"><span data-stu-id="c5314-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="c5314-108">Zabezpieczanie parametrów lub danych wejściowych w ramach działań w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="c5314-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="c5314-109">Zabezpieczanie tooservices dostępu, który odbierania żądań z przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="c5314-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="c5314-110">Bezpieczny dostęp tootrigger</span><span class="sxs-lookup"><span data-stu-id="c5314-110">Secure access tootrigger</span></span>

<span data-ttu-id="c5314-111">Podczas pracy z aplikacji logiki, które są generowane na żądania HTTP ([żądania](../connectors/connectors-native-reqres.md) lub [Webhook](../connectors/connectors-native-webhook.md)), można ograniczyć dostęp tak, aby tylko autoryzowani klienci mogą wyzwalać hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c5314-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="c5314-112">Wszystkie żądania do aplikacji logiki są szyfrowane i chronione za pomocą protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="c5314-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="c5314-113">Sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="c5314-113">Shared Access Signature</span></span>

<span data-ttu-id="c5314-114">Każdy punkt końcowy żądania dla aplikacji logiki obejmuje [dostępu sygnatury dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) jako część hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c5314-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="c5314-115">Każdy adres URL zawiera `sp`, `sv`, i `sig` parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="c5314-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="c5314-116">Uprawnienia są określane przez `sp`, i odpowiada metod tooHTTP dozwolonych, `sv` jest toogenerate wersja użyta hello, i `sig` jest używane tooauthenticate tootrigger dostępu.</span><span class="sxs-lookup"><span data-stu-id="c5314-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="c5314-117">Podpis Hello jest generowany przy użyciu algorytmu hello SHA256 z kluczem tajnym na wszystkie właściwości i ścieżki adresu URL hello.</span><span class="sxs-lookup"><span data-stu-id="c5314-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="c5314-118">klucz tajny Hello nigdy nie jest widoczne i opublikowana i są przechowywane w zaszyfrowanej i przechowywane hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c5314-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="c5314-119">Aplikację logiki autoryzuje tylko wyzwalaczy, które zawiera prawidłowy podpis utworzone za pomocą hello klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="c5314-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="c5314-120">Ponowne generowanie kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="c5314-120">Regenerate access keys</span></span>

<span data-ttu-id="c5314-121">Można ponownie wygenerować nowy klucz bezpiecznego w dowolnym momencie za pośrednictwem portalu hello interfejsu API REST lub Azure.</span><span class="sxs-lookup"><span data-stu-id="c5314-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="c5314-122">Wszystkie bieżącego adresów URL, które zostały wygenerowane wcześniej przy użyciu starego klucza hello są aplikacji logiki hello toofire nieważne i nie będzie autoryzowany.</span><span class="sxs-lookup"><span data-stu-id="c5314-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="c5314-123">Hello portalu Azure Otwórz aplikację logiki hello ma tooregenerate klucza</span><span class="sxs-lookup"><span data-stu-id="c5314-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="c5314-124">Kliknij przycisk hello **klucze dostępu** elementu menu pod **ustawienia**</span><span class="sxs-lookup"><span data-stu-id="c5314-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="c5314-125">Wybierz hello tooregenerate klucza i pełny hello procesu</span><span class="sxs-lookup"><span data-stu-id="c5314-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="c5314-126">Adresy URL, który można pobrać po ponowne generowanie są podpisane za pomocą hello nowy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="c5314-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="c5314-127">Tworzenie adresów URL wywołania zwrotnego z datą wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="c5314-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="c5314-128">Adres URL hello w przypadku udostępniania innym osobom, można wygenerować adresy URL określone klucze i daty ważności, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c5314-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="c5314-129">Można następnie bezproblemowo przywracania kluczy lub zapewnienia toofire dostępu do aplikacji jest ograniczony tooa niektórych timespan.</span><span class="sxs-lookup"><span data-stu-id="c5314-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="c5314-130">Można określić datę wygaśnięcia dla danego adresu URL za pośrednictwem hello [logiki aplikacji interfejsu API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="c5314-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="c5314-131">W treści hello zawiera właściwości hello `NotAfter` jako ciąg daty JSON, który zwraca adres URL wywołania zwrotnego, który jest prawidłowy tylko do hello `NotAfter` daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="c5314-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="c5314-132">Tworzenie adresów URL z podstawowym lub pomocniczym klucz tajny</span><span class="sxs-lookup"><span data-stu-id="c5314-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="c5314-133">Podczas generowania lub umieszczanie na liście adresów URL wywołania zwrotnego na podstawie żądań wyzwalaczy, można także określić adres URL, hello który klucza toouse toosign.</span><span class="sxs-lookup"><span data-stu-id="c5314-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="c5314-134">Możesz wygenerować adresu URL podpisane przez określonego klucza za pomocą hello [logiki aplikacji interfejsu API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c5314-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="c5314-135">W treści hello zawiera właściwości hello `KeyType` jako `Primary` lub `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="c5314-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="c5314-136">Zwróci ono podpisane przez klucz zabezpieczeń hello określony adres URL.</span><span class="sxs-lookup"><span data-stu-id="c5314-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="c5314-137">Ogranicz przychodzących adresów IP</span><span class="sxs-lookup"><span data-stu-id="c5314-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="c5314-138">Ponadto toohello Shared Access Signature, warto zapoznać się z toorestrict wywoływanie aplikacji logiki tylko z określonym klientem.</span><span class="sxs-lookup"><span data-stu-id="c5314-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="c5314-139">Na przykład, jeśli zarządzasz punktu końcowego za pośrednictwem usługi Azure API Management, można ograniczyć hello logiki aplikacji tooonly Zaakceptuj Żądanie hello, gdy hello żądanie pochodzi z adresu IP wystąpienia interfejsu API zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="c5314-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="c5314-140">To ustawienie można skonfigurować w ramach ustawień aplikacji logiki hello:</span><span class="sxs-lookup"><span data-stu-id="c5314-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="c5314-141">Hello portalu Azure Otwórz aplikację logiki hello ma ograniczenia adresu IP tooadd</span><span class="sxs-lookup"><span data-stu-id="c5314-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="c5314-142">Kliknij przycisk hello **konfiguracji kontroli dostępu** elementu menu pod **ustawienia**</span><span class="sxs-lookup"><span data-stu-id="c5314-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="c5314-143">Określ listę hello toobe zakresów adresów IP zaakceptowane przez wyzwalacz hello</span><span class="sxs-lookup"><span data-stu-id="c5314-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="c5314-144">Prawidłowy zakres IP ma hello format `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="c5314-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="c5314-145">Witaj logiki aplikacji tooonly fire jako aplikację logiki zagnieżdżonych, zaznacz hello **tylko innych aplikacji logiki** opcji.</span><span class="sxs-lookup"><span data-stu-id="c5314-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="c5314-146">Ta opcja powoduje zapisanie zasobów toohello pusta tablica, co oznacza, że tylko wywołania z hello samą usługą fire (aplikacje logiki nadrzędnego) pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c5314-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="c5314-147">Nadal można uruchomić aplikacji logiki z wyzwalaczem żądanie za pośrednictwem interfejsu API REST hello / zarządzania `/triggers/{triggerName}/run` niezależnie od adresu IP.</span><span class="sxs-lookup"><span data-stu-id="c5314-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="c5314-148">Ten scenariusz wymaga uwierzytelniania przed hello interfejsu API REST Azure, a wszystkie zdarzenia pojawiały się hello dziennik inspekcji Azure.</span><span class="sxs-lookup"><span data-stu-id="c5314-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="c5314-149">Ustaw dostęp do kontrolowania zasad odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="c5314-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="c5314-150">Ustawianie zakresów adresów IP w definicji zasobu hello</span><span class="sxs-lookup"><span data-stu-id="c5314-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="c5314-151">Jeśli używasz [Szablon wdrożenia](logic-apps-create-deploy-template.md) tooautomate wdrożeń, ustawienia zakres IP hello można skonfigurować na powitania zasobu szablon.</span><span class="sxs-lookup"><span data-stu-id="c5314-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="c5314-152">Dodawanie usługi Azure Active Directory, OAuth lub innych zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c5314-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="c5314-153">protokoły więcej autoryzacji na podstawie aplikacji logiki, tooadd [Azure API Management](https://azure.microsoft.com/services/api-management/) oferuje rozbudowane monitorowanie, zabezpieczeń, zasad i dokumentacji dla dowolnego punktu końcowego z tooexpose możliwości hello aplikacji logiki jako interfejs API.</span><span class="sxs-lookup"><span data-stu-id="c5314-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="c5314-154">Zarządzanie interfejsami API Azure mogą uwidaczniać publicznych lub prywatnych punktu końcowego dla aplikacji logiki hello, który może używać usługi Azure Active Directory, certyfikat, OAuth lub innych standardów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c5314-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="c5314-155">Po odebraniu żądania usługi Azure API Management przekazuje hello żądania toohello aplikacja logiki (wykonanie żadnych ograniczeń locie lub przekształcenia wymagane).</span><span class="sxs-lookup"><span data-stu-id="c5314-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="c5314-156">Można użyć hello przychodzące zakres IP ustawień na powitania logiki aplikacji tooonly umożliwiającej toobe aplikacji logiki hello wywołany z interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c5314-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="c5314-157">Bezpieczny dostęp do aplikacji logiki toomanage lub edycji</span><span class="sxs-lookup"><span data-stu-id="c5314-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="c5314-158">Tak, aby tylko określonym użytkownikom lub grupom są możliwe tooperform operacji dla zasobu hello, można ograniczyć dostęp toomanagement operacji w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c5314-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="c5314-159">Aplikacje logiki używać hello Azure [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) funkcji i można dostosować za pomocą hello tych samych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="c5314-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="c5314-160">Istnieje kilka wbudowanych ról, które można przypisać również członkowie tooas Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="c5314-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="c5314-161">**Współautor aplikacji logiki** — zapewnia dostęp tooview, edycji i aktualizacji aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c5314-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="c5314-162">Nie można usunąć zasobu hello ani wykonywać operacje administracyjne.</span><span class="sxs-lookup"><span data-stu-id="c5314-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="c5314-163">**Operator aplikacji logiki** — można wyświetlić aplikacji logiki hello i Historia uruchomień i włączanie/wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="c5314-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="c5314-164">Nie można edytować ani aktualizacji definicji hello.</span><span class="sxs-lookup"><span data-stu-id="c5314-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="c5314-165">Można również użyć [Blokada zasobu Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent, zmienianie lub usuwanie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="c5314-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="c5314-166">Ta funkcja jest przydatna tooprevent produkcji zasobów z zmiany i usunięcia.</span><span class="sxs-lookup"><span data-stu-id="c5314-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="c5314-167">Toocontents bezpieczny dostęp z hello Historia uruchomień</span><span class="sxs-lookup"><span data-stu-id="c5314-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="c5314-168">Z poprzednich zakresów adresów IP toospecific działa, można ograniczyć toocontents dostępu do danych wejściowych lub wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c5314-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="c5314-169">Wszystkie dane w ramach wykonywania przepływu pracy są szyfrowane przesyłanych i przechowywanych.</span><span class="sxs-lookup"><span data-stu-id="c5314-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="c5314-170">Gdy historii toorun połączeń, usługa hello uwierzytelnia Żądanie hello i udostępnia łącza toohello żądania i odpowiedzi wejściami i wyjściami.</span><span class="sxs-lookup"><span data-stu-id="c5314-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="c5314-171">To łącze może być chronione żądań tak tylko zawartość hello powrócić tooview zawartości z wyznaczonych zakresu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c5314-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="c5314-172">Ta funkcja służy do kontroli dostępu dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="c5314-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="c5314-173">Można nawet określić adres IP, takich jak `0.0.0.0` , nikt nie mógł uzyskać dostępu do danych wejściowych/wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c5314-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="c5314-174">Tylko osoby z uprawnieniami administratora może usunąć to ograniczenie, zapewniając możliwość powitania dla zawartości tooworkflow dostępu "just-in-time".</span><span class="sxs-lookup"><span data-stu-id="c5314-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="c5314-175">To ustawienie można skonfigurować w ramach ustawienia zasobów hello hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="c5314-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="c5314-176">Hello portalu Azure Otwórz aplikację logiki hello ma ograniczenia adresu IP tooadd</span><span class="sxs-lookup"><span data-stu-id="c5314-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="c5314-177">Kliknij przycisk hello **konfiguracji kontroli dostępu** elementu menu pod **ustawienia**</span><span class="sxs-lookup"><span data-stu-id="c5314-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="c5314-178">Określ listę hello zakresy adresów IP dla toocontent dostępu</span><span class="sxs-lookup"><span data-stu-id="c5314-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="c5314-179">Ustawianie zakresów adresów IP w definicji zasobu hello</span><span class="sxs-lookup"><span data-stu-id="c5314-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="c5314-180">Jeśli używasz [Szablon wdrożenia](logic-apps-create-deploy-template.md) tooautomate wdrożeń, ustawienia zakres IP hello można skonfigurować na powitania zasobu szablon.</span><span class="sxs-lookup"><span data-stu-id="c5314-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="c5314-181">Zabezpieczanie parametry i dane wejściowe w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="c5314-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="c5314-182">Możesz tooparameterize niektórych aspektów definicję przepływu pracy dla wdrażania w środowiskach.</span><span class="sxs-lookup"><span data-stu-id="c5314-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="c5314-183">Ponadto niektóre parametry mogą być bezpiecznego parametrów, które nie mają tooappear podczas edytowania przepływu pracy, takich jak identyfikator klienta i klucz tajny klienta dla [uwierzytelniania usługi Azure Active Directory](../connectors/connectors-native-http.md#authentication) akcji HTTP.</span><span class="sxs-lookup"><span data-stu-id="c5314-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="c5314-184">Przy użyciu parametrów i bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c5314-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="c5314-185">tooaccess hello wartości parametru zasobów w czasie wykonywania, hello [język definicji przepływu pracy](http://aka.ms/logicappsdocs) zapewnia `@parameters()` operacji.</span><span class="sxs-lookup"><span data-stu-id="c5314-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="c5314-186">Można również [Określ parametry szablonu wdrażania zasobów hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="c5314-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="c5314-187">Ale jeśli określony typ parametru hello jako `securestring`, parametr hello nie będą zwracane z hello reszty hello definicji zasobu i nie będzie dostępny, wyświetlając zasobów powitania po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="c5314-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="c5314-188">Jeśli parametr jest używany w nagłówkach hello lub treści żądania, parametr hello mogą być widoczne uzyskując dostęp do historii hello Uruchom i wychodzących żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="c5314-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="c5314-189">Należy zasad dostępu do zawartości tooset się odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="c5314-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="c5314-190">Nagłówki autoryzacji nie są widoczne za pośrednictwem wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c5314-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="c5314-191">Dlatego jeśli klucz tajny hello jest używany istnieje, klucz tajny hello nie jest pobieranie.</span><span class="sxs-lookup"><span data-stu-id="c5314-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="c5314-192">Szablon wdrożenia zasobów z kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="c5314-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="c5314-193">Witaj poniższy przykład przedstawia wdrożenia, który odwołuje się do parametru secure `secret` w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c5314-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="c5314-194">W pliku parametrów oddzielne można określić wartość środowiska hello hello `secret`, lub użyj [KeyVault Menedżera zasobów Azure](../azure-resource-manager/resource-manager-keyvault-parameter.md) kluczy tajnych tooretrieve na wdrażanie czasu.</span><span class="sxs-lookup"><span data-stu-id="c5314-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="c5314-195">Bezpieczny dostęp do odbierania żądań tooservices z przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="c5314-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="c5314-196">Istnieje wiele sposobów toohelp są bezpieczne, dowolną aplikację logiki hello punktu końcowego wymaga tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c5314-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="c5314-197">Przy użyciu uwierzytelniania w odpowiedzi na żądania wychodzącego</span><span class="sxs-lookup"><span data-stu-id="c5314-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="c5314-198">Podczas pracy z HTTP, HTTP + Swagger (otwarty interfejs API) lub elementu Webhook akcji, możesz dodać wysyłane żądania toohello uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="c5314-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="c5314-199">Mogą obejmować uwierzytelnianie podstawowe, uwierzytelnianie certyfikatu lub uwierzytelniania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5314-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="c5314-200">Szczegóły dotyczące sposobu tooconfigure tego uwierzytelniania można znaleźć [w tym artykule](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="c5314-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="c5314-201">Ograniczenia adresów IP aplikacji toologic dostępu</span><span class="sxs-lookup"><span data-stu-id="c5314-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="c5314-202">Wywołania z aplikacji logiki pochodzą z określonego zestawu adresów IP dla regionu.</span><span class="sxs-lookup"><span data-stu-id="c5314-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="c5314-203">Możesz dodać dodatkowe filtrowania tooonly akceptowania żądań od wyznaczonych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c5314-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="c5314-204">Aby uzyskać listę adresów IP, zobacz [limity aplikacji logiki i konfiguracji](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="c5314-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="c5314-205">Łączność lokalna</span><span class="sxs-lookup"><span data-stu-id="c5314-205">On-premises connectivity</span></span>

<span data-ttu-id="c5314-206">Aplikacje logiki mają integracji z kilku usług tooprovide bezpieczny i niezawodny lokalnej komunikacji.</span><span class="sxs-lookup"><span data-stu-id="c5314-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="c5314-207">Brama danych lokalnych</span><span class="sxs-lookup"><span data-stu-id="c5314-207">On-premises data gateway</span></span>

<span data-ttu-id="c5314-208">Wiele łączników zarządzanych dla usługi logic apps Podaj bezpieczna łączność systemów lokalnych tooon, w tym systemie plików, SQL, SharePoint i bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="c5314-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="c5314-209">Brama Hello przekazuje dane z lokalnych źródeł w kanałach zaszyfrowane za pomocą hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c5314-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="c5314-210">Cały ruch pochodzi jako bezpieczny ruch wychodzący z hello bramy agenta.</span><span class="sxs-lookup"><span data-stu-id="c5314-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="c5314-211">Dowiedz się więcej o [działanie bramy danych hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="c5314-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="c5314-212">Usługa Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c5314-212">Azure API Management</span></span>

<span data-ttu-id="c5314-213">[Zarządzanie interfejsami API Azure](https://azure.microsoft.com/services/api-management/) ma opcji łączności lokalnie, w tym site-to-site VPN i ExpressRoute integracji zabezpieczonych systemów lokalnych tooon serwera proxy i komunikacji.</span><span class="sxs-lookup"><span data-stu-id="c5314-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="c5314-214">W hello projektanta aplikacji logiki możesz szybko zaznaczyć interfejs API widoczne z usługi Azure API Management w przepływie pracy, zapewniając systemów lokalnych tooon szybki dostęp.</span><span class="sxs-lookup"><span data-stu-id="c5314-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="c5314-215">Połączenia hybrydowe z usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="c5314-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="c5314-216">Funkcja hello lokalnymi hybrydowego połączenia dla interfejsu API Azure i Web apps toocommunicate lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c5314-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="c5314-217">Więcej informacji dotyczących połączeń hybrydowych i jak można znaleźć tooconfigure [w tym artykule](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c5314-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5314-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5314-218">Next steps</span></span>
[<span data-ttu-id="c5314-219">Tworzenie szablonu wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c5314-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="c5314-220">Obsługa wyjątków</span><span class="sxs-lookup"><span data-stu-id="c5314-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="c5314-221">Monitorowanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="c5314-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="c5314-222">Diagnozowanie błędów aplikacji logiki i problemy</span><span class="sxs-lookup"><span data-stu-id="c5314-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
