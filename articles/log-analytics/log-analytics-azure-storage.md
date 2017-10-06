---
title: "aaaCollect Azure usługi Dzienniki i metryki dla Log Analytics | Dokumentacja firmy Microsoft"
description: "Skonfiguruj diagnostyki na zasobów Azure toowrite dzienniki i metryki tooLog Analytics."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Zbieranie dzienników usługi Azure i metryk do użycia w analizy dzienników

Istnieją cztery różne sposoby zbierania dzienników i metryki dla usług Azure:

1. Diagnostyka Azure bezpośrednie tooLog Analytics (*diagnostyki* w poniższej tabeli hello)
2. Diagnostyka Azure tooAzure magazynu tooLog Analytics (*magazynu* w poniższej tabeli hello)
3. Łączniki dla usług Azure (*łączniki* w poniższej tabeli hello)
4. Skrypty toocollect, a następnie post danych do analizy dzienników (puste wartości w hello w poniższej tabeli i usług, które nie są wymienione)


| Usługa                 | Typ zasobu                           | Dzienniki        | Metryki     | Rozwiązanie |
| --- | --- | --- | --- | --- |
| Bramy aplikacji    | Microsoft.Network/applicationGateways   | Diagnostyka | Diagnostyka | [Analiza bramy aplikacji Azure](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Usługa Application insights    |                                         | Łącznik   | Łącznik   | [Application Insights łącznik](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (wersja zapoznawcza) |
| Konta usługi Automation     | Microsoft.Automation/AutomationAccounts | Diagnostyka |             | [Więcej informacji](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Konta usługi partia zadań          | Microsoft.Batch/batchAccounts           | Diagnostyka | Diagnostyka | |
| Usługi w chmurze klasycznego  |                                         | Magazyn     |             | [Więcej informacji](log-analytics-azure-storage-iis-table.md) |
| Usługi poznawcze      | Microsoft.CognitiveServices/accounts    |             | Diagnostyka | |
| Data Lake analytics     | Microsoft.DataLakeAnalytics/accounts    | Diagnostyka |             | |
| Data Lake store         | Microsoft.DataLakeStore/accounts        | Diagnostyka |             | |
| Przestrzeń nazw Centrum zdarzeń     | Microsoft.EventHub/namespaces           | Diagnostyka | Diagnostyka | |
| Centra IoT                | Microsoft.Devices/IotHubs               |             | Diagnostyka | |
| Usługa Key Vault               | Microsoft.KeyVault/vaults               | Diagnostyka |             | [KeyVault analityka](log-analytics-azure-key-vault.md) |
| Moduły równoważenia obciążenia          | Microsoft.Network/loadBalancers         | Diagnostyka |             |  |
| Logic Apps              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Diagnostyka | Diagnostyka | |
| Grupy zabezpieczeń sieci | Microsoft.Network/networksecuritygroups | Diagnostyka |             | [Grupy zabezpieczeń sieci Azure analityka](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Magazyny odzyskiwania         | Microsoft.RecoveryServices/vaults       |             |             | [Usługa Azure Recovery usługi Analytics (wersja zapoznawcza)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Usługi wyszukiwania         | Microsoft.Search/searchServices         | Diagnostyka | Diagnostyka | |
| Przestrzeń nazw magistrali usług   | Microsoft.ServiceBus/namespaces         | Diagnostyka | Diagnostyka | [Analiza magistrali usług (wersja zapoznawcza)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Magazyn     |             | [Usługa sieci szkieletowej Analytics (wersja zapoznawcza)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Diagnostyka | [Analiza Azure SQL (wersja zapoznawcza)](log-analytics-azure-sql.md) |
| Magazyn                 |                                         |             | Skrypt      | [Usługa Azure Storage Analytics (wersja zapoznawcza)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Maszyny wirtualne        | Microsoft.Compute/virtualMachines       | Wewnętrzny   | Wewnętrzny <br> Diagnostyka  | |
| Zestawy skalowania maszyn wirtualnych | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Diagnostyka | |
| Farmach serwerów sieci Web        | Microsoft.Web/serverfarms               |             | Diagnostyka | |
| Witryny sieci Web               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Diagnostyka | [Analiza aplikacji sieci Web platformy Azure (wersja zapoznawcza)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Do monitorowania maszyn wirtualnych platformy Azure (Linux i Windows), zaleca się zainstalowanie hello [rozszerzenia maszyny Wirtualnej analizy dziennika](log-analytics-azure-vm-extension.md). Hello agent dostarcza szczegółowe informacje zebrane w maszynach wirtualnych. Można również użyć rozszerzenia powitania dla zestawy skalowania maszyny wirtualnej.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Diagnostyka Azure bezpośredniego tooLog analityka
Wiele zasobów platformy Azure są dzienników diagnostycznych może toowrite i metryki bezpośrednio tooLog analityka jest to preferowany hello sposób zbierania danych hello w celu analizy. Podczas korzystania z diagnostyki Azure, dane są zapisywane bezpośrednio tooLog analizy i nie ma toostorage nie konieczności toofirst zapisu hello danych.

Zasobów platformy Azure, które obsługują [Azure monitor](../monitoring-and-diagnostics/monitoring-overview.md) może wysłać ich dzienniki i metryki bezpośrednio tooLog Analytics.

* Witaj informacji z dostępnymi metrykami hello znajduje się zbyt[obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Szczegóły hello hello dostępne dzienniki, można znaleźć zbyt[obsługiwanych usług i schematu dla dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Włączanie diagnostyki przy użyciu programu PowerShell
Witaj listopada 2016 (v2.3.0) lub nowszej wersji usługi [programu Azure PowerShell](/powershell/azure/overview).

Witaj, po PowerShell przykładzie pokazano sposób toouse [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable diagnostyki w grupie zabezpieczeń sieci. Witaj same podejście działa w przypadku wszystkich obsługiwanych zasobów — Ustawianie `$resourceId` toohello identyfikator zasobu ma tooenable diagnostycznych dla zasobu hello.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Włącz diagnostykę z szablonami usługi Resource Manager

Diagnostyka tooenable do zasobu, gdy jest tworzona i diagnostyki hello wysłali tooyour obszaru roboczego analizy dzienników, których można użyć szablonu toohello podobne, jeden poniżej. W tym przykładzie jest dla konta automatyzacji, ale działa dla wszystkich obsługiwanych typów zasobów.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Diagnostyka Azure toostorage, a następnie tooLog analityka

Do zbierania dzienników z w niektórych zasobów, jego jest możliwe toosend hello dzienniki tooAzure magazynu, a następnie skonfiguruj analizy dzienników tooread hello dzienniki z magazynu.

Analiza dzienników można użyć tego podejścia diagnostyki toocollect z usługi Azure storage dla hello zasobów i dzienników:

| Zasób | Dzienniki |
| --- | --- |
| Service Fabric |ETWEvent <br> Zdarzeń operacyjnych <br> Zdarzenie niezawodnego aktora <br> Zdarzenie niezawodne usługi |
| Maszyny wirtualne |Systemu Linux <br> Zdarzenie systemu Windows <br> Dziennik IIS <br> ETWEvent systemu Windows |
| Role sieci Web <br> Role procesów roboczych |Systemu Linux <br> Zdarzenie systemu Windows <br> Dziennik IIS <br> ETWEvent systemu Windows |

> [!NOTE]
> Naliczane są opłaty szybkości normalne danych platformy Azure dla magazynu i transakcji wysyłanie danych diagnostycznych tooa konta magazynu i podczas analizy dzienników odczytuje hello dane z konta magazynu.
>
>

Zobacz [magazyn obiektów blob służy do przechowywania usług IIS i tabeli dla zdarzeń](log-analytics-azure-storage-iis-table.md) toolearn więcej informacji na temat sposobu analizy dzienników mogą zbierać Dzienniki te.

## <a name="connectors-for-azure-services"></a>Łączniki dla usług Azure

Jest łącznikiem usługi Application Insights, dzięki czemu dane zebrane przez wysyłane tooLog Analytics toobe usługi Application Insights.

Dowiedz się więcej o hello [łącznika usługi Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Skrypty toocollect i post danych tooLog Analytics

Dla usług Azure, które nie udostępniają tooLog sposób bezpośredniego toosend dzienniki i metryki Analytics można użyć toocollect skryptów automatyzacji Azure hello dziennika i metryki. Witaj Hello skrypt może następnie wyślij hello danych tooLog Analytics przy użyciu [modułów zbierających dane interfejsu API](log-analytics-data-collector-api.md)

ma galerii szablonu Azure Hello [przykłady użycia usługi Automatyzacja Azure](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect danych z usług i wysłanie go tooLog Analytics.

## <a name="next-steps"></a>Następne kroki

* [Użyj magazynu obiektów blob dla usług IIS i tabeli magazynu dla zdarzeń](log-analytics-azure-storage-iis-table.md) tooread hello dzienniki dla usług Azure, które zapisać diagnostyki tootable magazynu lub IIS rejestruje napisane tooblob magazynu.
* [Włącz rozwiązań](log-analytics-add-solutions.md) tooprovide wgląd w dane hello.
* [Użyj zapytań wyszukiwania](log-analytics-log-searches.md) tooanalyze hello danych.
