---
title: "Użyj akcji skalowania automatycznego do wysyłania wiadomości e-mail i elementu webhook powiadomień o alertach. | Microsoft Docs"
description: "Zobacz temat jak korzystać z akcji skalowania automatycznego połączeń telefonicznych z adresu URL sieci web lub wysyłania powiadomień e-mail w monitorze Azure. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="03af4-104">Umożliwia wysyłanie poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure akcji skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="03af4-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="03af4-105">W tym artykule opisano, jak skonfigurowaniu wyzwalaczy tak, aby można było wywołać adresu URL sieci web określonego lub wysyłania wiadomości e-mail w oparciu akcji skalowania automatycznego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="03af4-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="03af4-106">elementów webhook</span><span class="sxs-lookup"><span data-stu-id="03af4-106">Webhooks</span></span>
<span data-ttu-id="03af4-107">Elementów Webhook pozwalają kierować Azure powiadomień o alertach do innych systemów przetwarzania końcowego lub niestandardowych powiadomień.</span><span class="sxs-lookup"><span data-stu-id="03af4-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="03af4-108">Na przykład routingu alertu do usług, które może obsłużyć przychodzącego żądania sieci web wysyłania SMS, dziennik błędów, powiadomi zespołu za pomocą rozmowy i wiadomości usługi itp. Identyfikator URI elementu webhook musi być prawidłowy punkt końcowy HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="03af4-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="03af4-109">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="03af4-109">Email</span></span>
<span data-ttu-id="03af4-110">Może być wysyłana wiadomość e-mail do dowolnego adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="03af4-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="03af4-111">Administratorzy i współadministratorzy subskrypcji, w którym jest uruchomiona reguła również zostanie powiadomiony.</span><span class="sxs-lookup"><span data-stu-id="03af4-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="03af4-112">Usługi w chmurze i aplikacje sieci Web</span><span class="sxs-lookup"><span data-stu-id="03af4-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="03af4-113">Użytkownik może zdecydować się na z portalu Azure dla farmy serwerów (aplikacje sieci Web) i usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="03af4-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="03af4-114">Wybierz **skalowanie przez** metryki.</span><span class="sxs-lookup"><span data-stu-id="03af4-114">Choose the **scale by** metric.</span></span>

![Skalowanie przez](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="03af4-116">Zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="03af4-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="03af4-117">W przypadku nowszych maszyn wirtualnych utworzonych za pomocą Menedżera zasobów (zestawy skalowania maszyny wirtualnej) można skonfigurować to przy użyciu interfejsu API REST, szablony usługi Resource Manager, programu PowerShell i interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="03af4-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="03af4-118">Interfejs portalu nie jest jeszcze dostępna.</span><span class="sxs-lookup"><span data-stu-id="03af4-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="03af4-119">Korzystając z interfejsu API REST lub Menedżera zasobów szablonu, obejmują elementu powiadomienia o następujących opcji.</span><span class="sxs-lookup"><span data-stu-id="03af4-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="03af4-120">Pole</span><span class="sxs-lookup"><span data-stu-id="03af4-120">Field</span></span> | <span data-ttu-id="03af4-121">Obowiązkowe?</span><span class="sxs-lookup"><span data-stu-id="03af4-121">Mandatory?</span></span> | <span data-ttu-id="03af4-122">Opis</span><span class="sxs-lookup"><span data-stu-id="03af4-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03af4-123">Operacja</span><span class="sxs-lookup"><span data-stu-id="03af4-123">operation</span></span> |<span data-ttu-id="03af4-124">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-124">yes</span></span> |<span data-ttu-id="03af4-125">Wartość musi być "Skala"</span><span class="sxs-lookup"><span data-stu-id="03af4-125">value must be "Scale"</span></span> |
| <span data-ttu-id="03af4-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="03af4-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="03af4-127">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-127">yes</span></span> |<span data-ttu-id="03af4-128">Wartość musi być "prawda" lub "false"</span><span class="sxs-lookup"><span data-stu-id="03af4-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="03af4-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="03af4-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="03af4-130">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-130">yes</span></span> |<span data-ttu-id="03af4-131">Wartość musi być "prawda" lub "false"</span><span class="sxs-lookup"><span data-stu-id="03af4-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="03af4-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="03af4-132">customEmails</span></span> |<span data-ttu-id="03af4-133">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-133">yes</span></span> |<span data-ttu-id="03af4-134">wartość może być null [] lub tablicy ciągów wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="03af4-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="03af4-135">elementów webhook</span><span class="sxs-lookup"><span data-stu-id="03af4-135">webhooks</span></span> |<span data-ttu-id="03af4-136">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-136">yes</span></span> |<span data-ttu-id="03af4-137">wartość może być zerowy lub nieprawidłowy identyfikator Uri</span><span class="sxs-lookup"><span data-stu-id="03af4-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="03af4-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="03af4-138">serviceUri</span></span> |<span data-ttu-id="03af4-139">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-139">yes</span></span> |<span data-ttu-id="03af4-140">Nieprawidłowy identyfikator Uri protokołu https</span><span class="sxs-lookup"><span data-stu-id="03af4-140">a valid https Uri</span></span> |
| <span data-ttu-id="03af4-141">properties</span><span class="sxs-lookup"><span data-stu-id="03af4-141">properties</span></span> |<span data-ttu-id="03af4-142">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-142">yes</span></span> |<span data-ttu-id="03af4-143">Wartość musi być pusty {} lub może zawierać pary klucz wartość</span><span class="sxs-lookup"><span data-stu-id="03af4-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="03af4-144">Uwierzytelnianie w elementów webhook</span><span class="sxs-lookup"><span data-stu-id="03af4-144">Authentication in webhooks</span></span>
<span data-ttu-id="03af4-145">Elementu webhook uwierzytelniania z użyciem uwierzytelniania opartego na tokenie, w którym zapisać elementu webhook identyfikatora URI identyfikatorem token jako parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="03af4-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="03af4-146">Na przykład https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="03af4-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="03af4-147">Funkcja automatycznego skalowania powiadomień elementu webhook ładunku schematu</span><span class="sxs-lookup"><span data-stu-id="03af4-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="03af4-148">Podczas generowania powiadomień skalowania automatycznego następujące metadane jest uwzględnione w ładunku elementu webhook:</span><span class="sxs-lookup"><span data-stu-id="03af4-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="03af4-149">Pole</span><span class="sxs-lookup"><span data-stu-id="03af4-149">Field</span></span> | <span data-ttu-id="03af4-150">Obowiązkowe?</span><span class="sxs-lookup"><span data-stu-id="03af4-150">Mandatory?</span></span> | <span data-ttu-id="03af4-151">Opis</span><span class="sxs-lookup"><span data-stu-id="03af4-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03af4-152">status</span><span class="sxs-lookup"><span data-stu-id="03af4-152">status</span></span> |<span data-ttu-id="03af4-153">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-153">yes</span></span> |<span data-ttu-id="03af4-154">Stan wskazujący, że wygenerowano akcji skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="03af4-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="03af4-155">Operacja</span><span class="sxs-lookup"><span data-stu-id="03af4-155">operation</span></span> |<span data-ttu-id="03af4-156">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-156">yes</span></span> |<span data-ttu-id="03af4-157">Zwiększanie wystąpień będzie "Skaluj w poziomie" i w przypadku spadku wystąpień będzie "W skali"</span><span class="sxs-lookup"><span data-stu-id="03af4-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="03af4-158">Kontekst</span><span class="sxs-lookup"><span data-stu-id="03af4-158">context</span></span> |<span data-ttu-id="03af4-159">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-159">yes</span></span> |<span data-ttu-id="03af4-160">Kontekst akcji skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="03af4-160">The autoscale action context</span></span> |
| <span data-ttu-id="03af4-161">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="03af4-161">timestamp</span></span> |<span data-ttu-id="03af4-162">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-162">yes</span></span> |<span data-ttu-id="03af4-163">Sygnatura czasowa wyzwolenia akcji skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="03af4-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="03af4-164">id</span><span class="sxs-lookup"><span data-stu-id="03af4-164">id</span></span> |<span data-ttu-id="03af4-165">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-165">Yes</span></span> |<span data-ttu-id="03af4-166">Identyfikator Menedżera zasobów w ustawieniu skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="03af4-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="03af4-167">name</span><span class="sxs-lookup"><span data-stu-id="03af4-167">name</span></span> |<span data-ttu-id="03af4-168">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-168">Yes</span></span> |<span data-ttu-id="03af4-169">Nazwa ustawienia skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="03af4-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="03af4-170">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="03af4-170">details</span></span> |<span data-ttu-id="03af4-171">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-171">Yes</span></span> |<span data-ttu-id="03af4-172">Opis akcji, która miała usługi skalowania automatycznego i zmianę liczby wystąpień</span><span class="sxs-lookup"><span data-stu-id="03af4-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="03af4-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="03af4-173">subscriptionId</span></span> |<span data-ttu-id="03af4-174">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-174">Yes</span></span> |<span data-ttu-id="03af4-175">Identyfikator zasobu docelowego, na którym wykonywane jest skalowanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="03af4-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="03af4-176">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="03af4-176">resourceGroupName</span></span> |<span data-ttu-id="03af4-177">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-177">Yes</span></span> |<span data-ttu-id="03af4-178">Nazwa grupy zasobów zasobu docelowego, na którym wykonywane jest skalowanie</span><span class="sxs-lookup"><span data-stu-id="03af4-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="03af4-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="03af4-179">resourceName</span></span> |<span data-ttu-id="03af4-180">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-180">Yes</span></span> |<span data-ttu-id="03af4-181">Nazwa zasobu docelowego, na którym wykonywane jest skalowanie</span><span class="sxs-lookup"><span data-stu-id="03af4-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="03af4-182">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="03af4-182">resourceType</span></span> |<span data-ttu-id="03af4-183">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-183">Yes</span></span> |<span data-ttu-id="03af4-184">Trzy obsługiwane wartości: "microsoft.classiccompute/domainnames/slots/roles" - role usługi w chmurze, "microsoft.compute/virtualmachinescalesets" - zestawy skalowania maszyny wirtualnej i "Microsoft.Web/serverfarms" - aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="03af4-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="03af4-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="03af4-185">resourceId</span></span> |<span data-ttu-id="03af4-186">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-186">Yes</span></span> |<span data-ttu-id="03af4-187">Identyfikator zasobu docelowego, na którym wykonywane jest skalowanie usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03af4-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="03af4-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="03af4-188">portalLink</span></span> |<span data-ttu-id="03af4-189">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-189">Yes</span></span> |<span data-ttu-id="03af4-190">Azure portalu łącze na stronie Podsumowanie zasób docelowy</span><span class="sxs-lookup"><span data-stu-id="03af4-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="03af4-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="03af4-191">oldCapacity</span></span> |<span data-ttu-id="03af4-192">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-192">Yes</span></span> |<span data-ttu-id="03af4-193">Bieżąca (stare) liczbę wystąpień podczas skalowania automatycznego trwało akcji skalowania</span><span class="sxs-lookup"><span data-stu-id="03af4-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="03af4-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="03af4-194">newCapacity</span></span> |<span data-ttu-id="03af4-195">Tak</span><span class="sxs-lookup"><span data-stu-id="03af4-195">Yes</span></span> |<span data-ttu-id="03af4-196">Nowe liczba wystąpień skalowania automatycznego skalowania zasobu</span><span class="sxs-lookup"><span data-stu-id="03af4-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="03af4-197">Właściwości</span><span class="sxs-lookup"><span data-stu-id="03af4-197">Properties</span></span> |<span data-ttu-id="03af4-198">Nie</span><span class="sxs-lookup"><span data-stu-id="03af4-198">No</span></span> |<span data-ttu-id="03af4-199">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="03af4-199">Optional.</span></span> <span data-ttu-id="03af4-200">Zbiór < klucz, wartość > pary (na przykład słownika < String, String >).</span><span class="sxs-lookup"><span data-stu-id="03af4-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="03af4-201">Pole właściwości jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="03af4-201">The properties field is optional.</span></span> <span data-ttu-id="03af4-202">W niestandardowego interfejsu użytkownika lub przepływu pracy na podstawie aplikacji logiki można wprowadzić klucze i wartości, które mogą zostać przekazane za pomocą ładunku.</span><span class="sxs-lookup"><span data-stu-id="03af4-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="03af4-203">Alternatywny sposób, aby przekazywać właściwości niestandardowe wychodzących wywołanie elementu webhook jest użycie elementu webhook identyfikatora URI się (jako parametry kwerendy)</span><span class="sxs-lookup"><span data-stu-id="03af4-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
