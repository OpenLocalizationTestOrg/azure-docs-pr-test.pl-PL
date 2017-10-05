---
title: "Diagnostyka Azure dzienniki obsługiwane usługi i schematów | Dokumentacja firmy Microsoft"
description: "Zrozumienie obsługiwanych schematu usług i zdarzeń do dzienników diagnostycznych platformy Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: aa4fa6e0310b2725005dfa34e3225c89fb4282d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Obsługiwane usługi, schematy i kategorie dzienników diagnostycznych platformy Azure

[Dzienniki diagnostyczne zasobów platformy Azure](monitoring-overview-of-diagnostic-logs.md) są dzienniki emitowane przez zasobów platformy Azure, opisujących operacji tego zasobu. Te dzienniki są typu zasobu określonego. W tym artykule firma Microsoft konspektu zestaw obsługiwanych usług i schematu zdarzeń dla zdarzenia emitowane przez poszczególnych usług. Ten artykuł zawiera także pełną listę kategorie dziennika dostępne na typ zasobu.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>Obsługiwane usługi i schematy do dzienników diagnostycznych zasobu
Schemat dla dzienników diagnostycznych zasobu różni się w zależności od kategorii zasobów i dziennika.   

| Usługa | Schemat & dokumentów |
| --- | --- |
| API Management | Schemat nie jest dostępna. |
| Bramy Application Gateway |[Rejestrowania diagnostyki bramy aplikacji](../application-gateway/application-gateway-diagnostics.md) |
| Azure Automation |[Analizy dzienników dla usługi Automatyzacja Azure](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Azure Batch |[Azure rejestrowania diagnostycznego partii](../batch/batch-diagnostics.md) |
| Informacje na temat technologii klienta | Schemat nie jest dostępna. |
| Content Delivery Network | Schemat nie jest dostępna. |
| CosmosDB | Schemat nie jest dostępna. |
| Data Lake Analytics |[Accessing diagnostic logs for Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) (Dostęp do dzienników diagnostycznych usługi Azure Data Lake Analytics) |
| Data Lake Store |[Uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Store](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Usługa Event Hubs |[Azure Event Hubs dzienników diagnostycznych](../event-hubs/event-hubs-diagnostic-logs.md) |
| Usługa Key Vault |[Funkcja rejestrowania usługi Azure Key Vault](../key-vault/key-vault-logging.md) |
| Moduł równoważenia obciążenia |[Analiza dzienników dotyczących usługi Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md) |
| Logic Apps |[Logic Apps — niestandardowy schemat śledzenia B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| Grupy zabezpieczeń sieci |[Usługa Log Analytics dla sieciowych grup zabezpieczeń](../virtual-network/virtual-network-nsg-manage-log.md) |
| Recovery Services | Schemat nie jest dostępna.|
| Wyszukiwanie |[Włączanie i używanie analizy ruchu wyszukiwania](../search/search-traffic-analytics.md) |
| Zarządzanie serwerem | Schemat nie jest dostępna. |
| Service Bus |[Azure Service Bus dzienników diagnostycznych](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| Stream Analytics |[Dzienniki diagnostyczne zadania](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |

## <a name="supported-log-categories-per-resource-type"></a>Obsługiwane kategorie dziennika na typ zasobu
|Typ zasobu|Kategoria|Nazwa wyświetlana kategorii|
|---|---|---|
|Microsoft.ApiManagement/service|GatewayLogs|Dzienniki związane z ApiManagement bramy|
|Microsoft.Automation/automationAccounts|JobLogs|Rejestruje zadania|
|Microsoft.Automation/automationAccounts|JobStreams|Strumienie zadania|
|Microsoft.Automation/automationAccounts|DscNodeStatus|Stan węzła DSC|
|Microsoft.Batch/batchAccounts|ServiceLog|Dzienniki usługi|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Pobiera metryki punktu końcowego, np. przepustowości, transfer danych wychodzących,... itd.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataLakeAnalytics/accounts|Inspekcja|Dzienniki inspekcji|
|Microsoft.DataLakeAnalytics/accounts|Żądania|Dzienniki żądań|
|Microsoft.DataLakeStore/accounts|Inspekcja|Dzienniki inspekcji|
|Microsoft.DataLakeStore/accounts|Żądania|Dzienniki żądań|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|Dzienniki archiwum|
|Microsoft.EventHub/namespaces|OperationalLogs|Operacyjne dzienniki|
|Microsoft.EventHub/namespaces|AutoScaleLogs|Dzienniki skalowania automatycznego|
|Microsoft.KeyVault/vaults|AuditEvent|Dzienniki inspekcji|
|Microsoft.Logic/workflows|Obiekt WorkflowRuntime|Zdarzenia diagnostyczne środowiska uruchomieniowego przepływu pracy|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|Zdarzenia śledzenia konta integracji|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|Zdarzenie sieciowej grupy zabezpieczeń|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|Licznik reguł sieciowej grupy zabezpieczeń|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|Zdarzenia alertu modułu równoważenia obciążenia|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|Stan kondycji sondę modułu równoważenia obciążenia|
|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|Dziennik dostępu bramy aplikacji|
|Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|Dziennik wydajności bramy aplikacji|
|Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|Dziennik zapory bramy aplikacji|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Kopia zapasowa Azure danych raportowania|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Zadania usługi Azure Site Recovery|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Usługi Azure Site Recovery zdarzenia|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Elementy replikowane usługi Azure Site Recovery|
|Microsoft.Search/searchServices|OperationLogs|Dzienniki operacji|
|Microsoft.ServiceBus/namespaces|OperationalLogs|Operacyjne dzienniki|
|Microsoft.StreamAnalytics/streamingjobs|Wykonanie|Wykonanie|
|Microsoft.StreamAnalytics/streamingjobs|Tworzenie|Tworzenie|

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się więcej o dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md)
* [Strumień zasobu dzienników diagnostycznych do **centra zdarzeń**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Zmień ustawienia diagnostyczne zasobu przy użyciu interfejsu API REST Azure monitora](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analizowanie dzienników z usługi Azure storage z analizy dzienników](../log-analytics/log-analytics-azure-storage.md)
