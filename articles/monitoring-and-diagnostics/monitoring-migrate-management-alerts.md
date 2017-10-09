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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Migrowanie Azure alerty Alerty dziennika tooActivity zdarzeń zarządzania


> [!WARNING]
> Alerty dotyczące zdarzeń zarządzania zostaną wyłączone na lub po 1 października. Jeśli te alerty i ich migracją, jeśli tak, użyj wskazówek hello poniżej toounderstand.
>
> 

## <a name="what-is-changing"></a>Co to jest zmieniany

Monitor Azure (poprzednio Azure Insights) oferowane toocreate możliwości alert wyzwolony wylogowuje zdarzeń zarządzania i generowane powiadomienia tooa elementu webhook adres URL lub adresy e-mail. Został utworzony dla jednej z tych alertów żadnego z następujących sposobów:
* W portalu Azure dotyczące określonych typów zasobów hello, w obszarze monitorowanie -> Alerty -> Dodaj alertu, gdzie "W alercie" jest ustawiona zbyt "Zdarzenia"
* Przez uruchomione polecenie cmdlet programu PowerShell Dodaj AzureRmLogAlertRule hello
* Za pomocą bezpośrednio [hello alertu interfejsu API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) odata.type = "ManagementEventRuleCondition" i dataSource.odata.type = "RuleManagementEventDataSource"
 
Witaj następujący skrypt programu PowerShell zwraca listę wszystkie alerty dotyczące zdarzeń zarządzania w Twojej subskrypcji, a także warunki hello na każdy alert.

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

Jeśli masz żadne alerty dotyczące zdarzeń zarządzania hello polecenia cmdlet programu PowerShell powyższe dane wyjściowe obejmują szereg komunikaty ostrzegawcze podobne do następującego:

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Te komunikaty ostrzegawcze można zignorować. Jeśli masz alerty dotyczące zdarzeń zarządzania, hello wyjściem tego polecenia cmdlet programu PowerShell będzie wyglądać następująco:

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

Każdy alert jest oddzielona linię kropkowaną i szczegółowe informacje zawierają identyfikator zasobu hello hello alert i hello określonej reguły monitorowanych.

Ta funkcja została przekształcona zbyt[alerty dziennika aktywności monitora Azure](monitoring-activity-log-alerts.md). Te nowe alerty umożliwiają tooset warunek zdarzeń dziennika aktywności i otrzymasz powiadomienie, gdy jest to nowe zdarzenie jest zgodna z hello warunku. Oferują one również kilka ulepszeń z alertów dotyczących zdarzeń zarządzania:
* Ponowne użycie grupy odbiorców powiadomień ("działania") przez wiele alertów za pomocą [grupy akcji](monitoring-action-groups.md), zmniejsza się złożoność hello zmian, który powinien zostać wyświetlony alert.
* Zostanie wyświetlone powiadomienie, bezpośrednio na telefonie z grupami akcji przy użyciu programu SMS.
* Możesz [tworzyć alerty dziennika aktywności z szablonami usługi Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* Warunki można tworzyć z większą elastyczność i złożoność toomeet określonych potrzeb.
* Powiadomienia są dostarczane szybciej.
 
## <a name="how-toomigrate"></a>Jak toomigrate
 
toocreate nowe działanie alertów dziennika, możesz:
* Wykonaj [naszego przewodnika w sposób toocreate alertu w hello portalu Azure](monitoring-activity-log-alerts.md)
* Dowiedz się, jak za[utworzyć alert przy użyciu szablonu usługi Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Alerty dotyczące zdarzeń zarządzania, które wcześniej zostały utworzone nie będzie automatycznie zmigrowane tooActivity dziennika alerty. Należy hello toouse poprzedzających alerty hello toolist skrypt programu PowerShell dotyczące zdarzeń zarządzania obecnie zostały skonfigurowane, a następnie ponownie ręcznie utworzyć je jako alertów dotyczących działań w dzienniku. Należy to zrobić przed 1 października, po którym alertów dotyczących zdarzeń zarządzania nie będą już widoczne w Twojej subskrypcji platformy Azure. Innych typów alertów Azure, w tym metryki alerty monitora Azure, alerty usługi Application Insights i analizy dzienników alerty są dotknięte tej zmiany. Jeśli masz pytania, opublikuj na powitania komentarze poniżej.


## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [dziennik aktywności](monitoring-overview-activity-logs.md)
* Skonfiguruj [alerty dziennika aktywności za pośrednictwem portalu Azure](monitoring-activity-log-alerts.md)
* Skonfiguruj [alerty dziennika aktywności za pomocą Menedżera zasobów](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Przejrzyj hello [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md)
* Dowiedz się więcej o [powiadomień usługi](monitoring-service-notifications.md)
* Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md)
