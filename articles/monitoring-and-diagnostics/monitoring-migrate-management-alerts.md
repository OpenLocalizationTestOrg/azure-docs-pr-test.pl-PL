---
title: "aaaMigrate Azure alerty na tooActivity zdarzeń zarządzania alertami dziennika | Dokumentacja firmy Microsoft"
description: "Alerty dotyczące zdarzeń zarządzania zostanie usunięty 1 października. Przygotuj przez Migrowanie istniejących alertów."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="6f146-104">Migrowanie Azure alerty Alerty dziennika tooActivity zdarzeń zarządzania</span><span class="sxs-lookup"><span data-stu-id="6f146-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="6f146-105">Alerty dotyczące zdarzeń zarządzania zostaną wyłączone na lub po 1 października.</span><span class="sxs-lookup"><span data-stu-id="6f146-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="6f146-106">Jeśli te alerty i ich migracją, jeśli tak, użyj wskazówek hello poniżej toounderstand.</span><span class="sxs-lookup"><span data-stu-id="6f146-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="6f146-107">Co to jest zmieniany</span><span class="sxs-lookup"><span data-stu-id="6f146-107">What is changing</span></span>

<span data-ttu-id="6f146-108">Monitor Azure (poprzednio Azure Insights) oferowane toocreate możliwości alert wyzwolony wylogowuje zdarzeń zarządzania i generowane powiadomienia tooa elementu webhook adres URL lub adresy e-mail.</span><span class="sxs-lookup"><span data-stu-id="6f146-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="6f146-109">Został utworzony dla jednej z tych alertów żadnego z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="6f146-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="6f146-110">W portalu Azure dotyczące określonych typów zasobów hello, w obszarze monitorowanie -> Alerty -> Dodaj alertu, gdzie "W alercie" jest ustawiona zbyt "Zdarzenia"</span><span class="sxs-lookup"><span data-stu-id="6f146-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="6f146-111">Przez uruchomione polecenie cmdlet programu PowerShell Dodaj AzureRmLogAlertRule hello</span><span class="sxs-lookup"><span data-stu-id="6f146-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="6f146-112">Za pomocą bezpośrednio [hello alertu interfejsu API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) odata.type = "ManagementEventRuleCondition" i dataSource.odata.type = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="6f146-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="6f146-113">Witaj następujący skrypt programu PowerShell zwraca listę wszystkie alerty dotyczące zdarzeń zarządzania w Twojej subskrypcji, a także warunki hello na każdy alert.</span><span class="sxs-lookup"><span data-stu-id="6f146-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

<span data-ttu-id="6f146-114">Jeśli masz żadne alerty dotyczące zdarzeń zarządzania hello polecenia cmdlet programu PowerShell powyższe dane wyjściowe obejmują szereg komunikaty ostrzegawcze podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="6f146-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="6f146-115">Te komunikaty ostrzegawcze można zignorować.</span><span class="sxs-lookup"><span data-stu-id="6f146-115">These warning messages can be ignored.</span></span> <span data-ttu-id="6f146-116">Jeśli masz alerty dotyczące zdarzeń zarządzania, hello wyjściem tego polecenia cmdlet programu PowerShell będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6f146-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

<span data-ttu-id="6f146-117">Każdy alert jest oddzielona linię kropkowaną i szczegółowe informacje zawierają identyfikator zasobu hello hello alert i hello określonej reguły monitorowanych.</span><span class="sxs-lookup"><span data-stu-id="6f146-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="6f146-118">Ta funkcja została przekształcona zbyt[alerty dziennika aktywności monitora Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6f146-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="6f146-119">Te nowe alerty umożliwiają tooset warunek zdarzeń dziennika aktywności i otrzymasz powiadomienie, gdy jest to nowe zdarzenie jest zgodna z hello warunku.</span><span class="sxs-lookup"><span data-stu-id="6f146-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="6f146-120">Oferują one również kilka ulepszeń z alertów dotyczących zdarzeń zarządzania:</span><span class="sxs-lookup"><span data-stu-id="6f146-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="6f146-121">Ponowne użycie grupy odbiorców powiadomień ("działania") przez wiele alertów za pomocą [grupy akcji](monitoring-action-groups.md), zmniejsza się złożoność hello zmian, który powinien zostać wyświetlony alert.</span><span class="sxs-lookup"><span data-stu-id="6f146-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="6f146-122">Zostanie wyświetlone powiadomienie, bezpośrednio na telefonie z grupami akcji przy użyciu programu SMS.</span><span class="sxs-lookup"><span data-stu-id="6f146-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="6f146-123">Możesz [tworzyć alerty dziennika aktywności z szablonami usługi Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="6f146-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="6f146-124">Warunki można tworzyć z większą elastyczność i złożoność toomeet określonych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="6f146-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="6f146-125">Powiadomienia są dostarczane szybciej.</span><span class="sxs-lookup"><span data-stu-id="6f146-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="6f146-126">Jak toomigrate</span><span class="sxs-lookup"><span data-stu-id="6f146-126">How toomigrate</span></span>
 
<span data-ttu-id="6f146-127">toocreate nowe działanie alertów dziennika, możesz:</span><span class="sxs-lookup"><span data-stu-id="6f146-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="6f146-128">Wykonaj [naszego przewodnika w sposób toocreate alertu w hello portalu Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="6f146-129">Dowiedz się, jak za[utworzyć alert przy użyciu szablonu usługi Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="6f146-130">Alerty dotyczące zdarzeń zarządzania, które wcześniej zostały utworzone nie będzie automatycznie zmigrowane tooActivity dziennika alerty.</span><span class="sxs-lookup"><span data-stu-id="6f146-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="6f146-131">Należy hello toouse poprzedzających alerty hello toolist skrypt programu PowerShell dotyczące zdarzeń zarządzania obecnie zostały skonfigurowane, a następnie ponownie ręcznie utworzyć je jako alertów dotyczących działań w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="6f146-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="6f146-132">Należy to zrobić przed 1 października, po którym alertów dotyczących zdarzeń zarządzania nie będą już widoczne w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f146-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="6f146-133">Innych typów alertów Azure, w tym metryki alerty monitora Azure, alerty usługi Application Insights i analizy dzienników alerty są dotknięte tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="6f146-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="6f146-134">Jeśli masz pytania, opublikuj na powitania komentarze poniżej.</span><span class="sxs-lookup"><span data-stu-id="6f146-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f146-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f146-135">Next steps</span></span>

* <span data-ttu-id="6f146-136">Dowiedz się więcej o [dziennik aktywności](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="6f146-137">Skonfiguruj [alerty dziennika aktywności za pośrednictwem portalu Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="6f146-138">Skonfiguruj [alerty dziennika aktywności za pomocą Menedżera zasobów](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="6f146-139">Przejrzyj hello [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="6f146-140">Dowiedz się więcej o [powiadomień usługi](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="6f146-141">Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="6f146-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
