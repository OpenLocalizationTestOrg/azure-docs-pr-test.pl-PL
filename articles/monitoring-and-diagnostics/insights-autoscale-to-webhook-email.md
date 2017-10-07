---
title: "aaaUse skalowania automatycznego akcje toosend poczty e-mail i elementu webhook powiadomień o alertach. | Microsoft Docs"
description: "Zobacz, jak toocall akcji skalowania automatycznego toouse adresy URL w sieci web lub wysyłania powiadomień e-mail w monitorze Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="a0f6b-104">Użyj automatycznego skalowania akcje toosend poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure</span><span class="sxs-lookup"><span data-stu-id="a0f6b-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="a0f6b-105">W tym artykule opisano, jak skonfigurowaniu wyzwalaczy tak, aby można było wywołać adresu URL sieci web określonego lub wysyłania wiadomości e-mail w oparciu akcji skalowania automatycznego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="a0f6b-106">elementów webhook</span><span class="sxs-lookup"><span data-stu-id="a0f6b-106">Webhooks</span></span>
<span data-ttu-id="a0f6b-107">Elementów Webhook pozwalają tooroute hello Azure powiadomień o alertach tooother systemów przetwarzania końcowego lub niestandardowych powiadomień.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="a0f6b-108">Na przykład routingu tooservices alertu hello, które może obsłużyć przychodzący sieci web żądania toosend programu SMS, usterki dziennika powiadamiać zespołu za pomocą rozmowy lub usługami wiadomości, webhook hello itp. identyfikator URI musi być prawidłowy punkt końcowy HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="a0f6b-109">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="a0f6b-109">Email</span></span>
<span data-ttu-id="a0f6b-110">Może być wysyłana wiadomość e-mail tooany prawidłowy adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="a0f6b-111">Administratorzy i współadministratorzy hello subskrypcji, którym jest uruchomiona reguła hello również otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="a0f6b-112">Usługi w chmurze i aplikacje sieci Web</span><span class="sxs-lookup"><span data-stu-id="a0f6b-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="a0f6b-113">Użytkownik może zgody na z portalu Azure hello farm serwerów (aplikacje sieci Web) i usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="a0f6b-114">Wybierz hello **skalowanie przez** metryki.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-114">Choose hello **scale by** metric.</span></span>

![Skalowanie przez](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="a0f6b-116">Zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a0f6b-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="a0f6b-117">W przypadku nowszych maszyn wirtualnych utworzonych za pomocą Menedżera zasobów (zestawy skalowania maszyny wirtualnej) można skonfigurować to przy użyciu interfejsu API REST, szablony usługi Resource Manager, programu PowerShell i interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="a0f6b-118">Interfejs portalu nie jest jeszcze dostępna.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="a0f6b-119">Korzystając z interfejsu API REST hello lub szablonu usługi Resource Manager, element include w hello powiadomienia o hello następujące opcje.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="a0f6b-120">Pole</span><span class="sxs-lookup"><span data-stu-id="a0f6b-120">Field</span></span> | <span data-ttu-id="a0f6b-121">Obowiązkowe?</span><span class="sxs-lookup"><span data-stu-id="a0f6b-121">Mandatory?</span></span> | <span data-ttu-id="a0f6b-122">Opis</span><span class="sxs-lookup"><span data-stu-id="a0f6b-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0f6b-123">Operacja</span><span class="sxs-lookup"><span data-stu-id="a0f6b-123">operation</span></span> |<span data-ttu-id="a0f6b-124">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-124">yes</span></span> |<span data-ttu-id="a0f6b-125">Wartość musi być "Skala"</span><span class="sxs-lookup"><span data-stu-id="a0f6b-125">value must be "Scale"</span></span> |
| <span data-ttu-id="a0f6b-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="a0f6b-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="a0f6b-127">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-127">yes</span></span> |<span data-ttu-id="a0f6b-128">Wartość musi być "prawda" lub "false"</span><span class="sxs-lookup"><span data-stu-id="a0f6b-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="a0f6b-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="a0f6b-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="a0f6b-130">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-130">yes</span></span> |<span data-ttu-id="a0f6b-131">Wartość musi być "prawda" lub "false"</span><span class="sxs-lookup"><span data-stu-id="a0f6b-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="a0f6b-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="a0f6b-132">customEmails</span></span> |<span data-ttu-id="a0f6b-133">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-133">yes</span></span> |<span data-ttu-id="a0f6b-134">wartość może być null [] lub tablicy ciągów wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="a0f6b-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="a0f6b-135">elementów webhook</span><span class="sxs-lookup"><span data-stu-id="a0f6b-135">webhooks</span></span> |<span data-ttu-id="a0f6b-136">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-136">yes</span></span> |<span data-ttu-id="a0f6b-137">wartość może być zerowy lub nieprawidłowy identyfikator Uri</span><span class="sxs-lookup"><span data-stu-id="a0f6b-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="a0f6b-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="a0f6b-138">serviceUri</span></span> |<span data-ttu-id="a0f6b-139">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-139">yes</span></span> |<span data-ttu-id="a0f6b-140">Nieprawidłowy identyfikator Uri protokołu https</span><span class="sxs-lookup"><span data-stu-id="a0f6b-140">a valid https Uri</span></span> |
| <span data-ttu-id="a0f6b-141">properties</span><span class="sxs-lookup"><span data-stu-id="a0f6b-141">properties</span></span> |<span data-ttu-id="a0f6b-142">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-142">yes</span></span> |<span data-ttu-id="a0f6b-143">Wartość musi być pusty {} lub może zawierać pary klucz wartość</span><span class="sxs-lookup"><span data-stu-id="a0f6b-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="a0f6b-144">Uwierzytelnianie w elementów webhook</span><span class="sxs-lookup"><span data-stu-id="a0f6b-144">Authentication in webhooks</span></span>
<span data-ttu-id="a0f6b-145">Element webhook Hello uwierzytelniania z użyciem uwierzytelniania opartego na tokenie, gdzie zapisać elementu webhook hello identyfikatora URI identyfikatorem token jako parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="a0f6b-146">Na przykład https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="a0f6b-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="a0f6b-147">Funkcja automatycznego skalowania powiadomień elementu webhook ładunku schematu</span><span class="sxs-lookup"><span data-stu-id="a0f6b-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="a0f6b-148">Podczas generowania powiadomień skalowania automatycznego hello hello następujące metadane znajduje się w ładunku webhook hello:</span><span class="sxs-lookup"><span data-stu-id="a0f6b-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="a0f6b-149">Pole</span><span class="sxs-lookup"><span data-stu-id="a0f6b-149">Field</span></span> | <span data-ttu-id="a0f6b-150">Obowiązkowe?</span><span class="sxs-lookup"><span data-stu-id="a0f6b-150">Mandatory?</span></span> | <span data-ttu-id="a0f6b-151">Opis</span><span class="sxs-lookup"><span data-stu-id="a0f6b-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0f6b-152">status</span><span class="sxs-lookup"><span data-stu-id="a0f6b-152">status</span></span> |<span data-ttu-id="a0f6b-153">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-153">yes</span></span> |<span data-ttu-id="a0f6b-154">Stan Hello, który wskazuje, że wygenerowano akcji skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="a0f6b-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="a0f6b-155">Operacja</span><span class="sxs-lookup"><span data-stu-id="a0f6b-155">operation</span></span> |<span data-ttu-id="a0f6b-156">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-156">yes</span></span> |<span data-ttu-id="a0f6b-157">Zwiększanie wystąpień będzie "Skaluj w poziomie" i w przypadku spadku wystąpień będzie "W skali"</span><span class="sxs-lookup"><span data-stu-id="a0f6b-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="a0f6b-158">Kontekst</span><span class="sxs-lookup"><span data-stu-id="a0f6b-158">context</span></span> |<span data-ttu-id="a0f6b-159">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-159">yes</span></span> |<span data-ttu-id="a0f6b-160">kontekst akcji skalowania automatycznego Hello</span><span class="sxs-lookup"><span data-stu-id="a0f6b-160">hello autoscale action context</span></span> |
| <span data-ttu-id="a0f6b-161">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="a0f6b-161">timestamp</span></span> |<span data-ttu-id="a0f6b-162">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-162">yes</span></span> |<span data-ttu-id="a0f6b-163">Sygnatura czasowa wyzwolenia hello akcji skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="a0f6b-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="a0f6b-164">id</span><span class="sxs-lookup"><span data-stu-id="a0f6b-164">id</span></span> |<span data-ttu-id="a0f6b-165">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-165">Yes</span></span> |<span data-ttu-id="a0f6b-166">Identyfikator Menedżera zasobów hello ustawieniu skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="a0f6b-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="a0f6b-167">name</span><span class="sxs-lookup"><span data-stu-id="a0f6b-167">name</span></span> |<span data-ttu-id="a0f6b-168">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-168">Yes</span></span> |<span data-ttu-id="a0f6b-169">Nazwa Hello hello ustawieniu skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="a0f6b-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="a0f6b-170">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="a0f6b-170">details</span></span> |<span data-ttu-id="a0f6b-171">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-171">Yes</span></span> |<span data-ttu-id="a0f6b-172">Wyjaśnienie działań hello hello automatycznego skalowania usługi trwało i hello zmiana liczby wystąpień hello</span><span class="sxs-lookup"><span data-stu-id="a0f6b-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="a0f6b-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a0f6b-173">subscriptionId</span></span> |<span data-ttu-id="a0f6b-174">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-174">Yes</span></span> |<span data-ttu-id="a0f6b-175">Identyfikator subskrypcji hello zasobu docelowego, który wykonywane jest skalowanie</span><span class="sxs-lookup"><span data-stu-id="a0f6b-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="a0f6b-176">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="a0f6b-176">resourceGroupName</span></span> |<span data-ttu-id="a0f6b-177">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-177">Yes</span></span> |<span data-ttu-id="a0f6b-178">Nazwa grupy zasobów zasobu docelowego hello wykonywane jest skalowanie</span><span class="sxs-lookup"><span data-stu-id="a0f6b-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="a0f6b-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="a0f6b-179">resourceName</span></span> |<span data-ttu-id="a0f6b-180">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-180">Yes</span></span> |<span data-ttu-id="a0f6b-181">Nazwa zasobu docelowego hello, że wykonywane jest skalowanie</span><span class="sxs-lookup"><span data-stu-id="a0f6b-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="a0f6b-182">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="a0f6b-182">resourceType</span></span> |<span data-ttu-id="a0f6b-183">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-183">Yes</span></span> |<span data-ttu-id="a0f6b-184">Witaj trzy obsługiwane wartości: "microsoft.classiccompute/domainnames/slots/roles" - role usługi w chmurze, "microsoft.compute/virtualmachinescalesets" - zestawy skalowania maszyny wirtualnej i "Microsoft.Web/serverfarms" - aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a0f6b-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="a0f6b-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="a0f6b-185">resourceId</span></span> |<span data-ttu-id="a0f6b-186">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-186">Yes</span></span> |<span data-ttu-id="a0f6b-187">Identyfikator zasobu docelowego hello, że wykonywane jest skalowanie Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="a0f6b-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="a0f6b-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="a0f6b-188">portalLink</span></span> |<span data-ttu-id="a0f6b-189">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-189">Yes</span></span> |<span data-ttu-id="a0f6b-190">Strona podsumowania toohello linku portalu Azure hello zasobu docelowego</span><span class="sxs-lookup"><span data-stu-id="a0f6b-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="a0f6b-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="a0f6b-191">oldCapacity</span></span> |<span data-ttu-id="a0f6b-192">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-192">Yes</span></span> |<span data-ttu-id="a0f6b-193">Witaj bieżącą (stare) liczbę wystąpień podczas skalowania automatycznego trwało akcji skalowania</span><span class="sxs-lookup"><span data-stu-id="a0f6b-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="a0f6b-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="a0f6b-194">newCapacity</span></span> |<span data-ttu-id="a0f6b-195">Tak</span><span class="sxs-lookup"><span data-stu-id="a0f6b-195">Yes</span></span> |<span data-ttu-id="a0f6b-196">Hello skalowania automatycznego zbyt skalowania zasobu hello nowe liczba wystąpień</span><span class="sxs-lookup"><span data-stu-id="a0f6b-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="a0f6b-197">Właściwości</span><span class="sxs-lookup"><span data-stu-id="a0f6b-197">Properties</span></span> |<span data-ttu-id="a0f6b-198">Nie</span><span class="sxs-lookup"><span data-stu-id="a0f6b-198">No</span></span> |<span data-ttu-id="a0f6b-199">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-199">Optional.</span></span> <span data-ttu-id="a0f6b-200">Zbiór < klucz, wartość > pary (na przykład słownika < String, String >).</span><span class="sxs-lookup"><span data-stu-id="a0f6b-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="a0f6b-201">pole właściwości Hello jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-201">hello properties field is optional.</span></span> <span data-ttu-id="a0f6b-202">W niestandardowego interfejsu użytkownika lub przepływu pracy na podstawie aplikacji logiki można wprowadzić klucze i wartości, które mogą zostać przekazane za pomocą hello ładunku.</span><span class="sxs-lookup"><span data-stu-id="a0f6b-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="a0f6b-203">Alternatywny sposób wywołania elementu webhook wychodzącego toohello kopii toopass właściwości niestandardowych jest toouse hello webhook identyfikatora URI się (jako parametry kwerendy)</span><span class="sxs-lookup"><span data-stu-id="a0f6b-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
