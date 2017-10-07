---
title: aaaMonitor operacje, zdarzenia i liczniki dla grup NSG | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooenable liczników, zdarzeń i operacyjne rejestrowania dla grupy NSG"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Usługa Log Analytics dla sieciowych grup zabezpieczeń

Możesz włączyć następujące kategorie dzienników diagnostycznych dla grup NSG hello:

* **Zdarzenie:** zawiera wpisy, dla których NSG reguły są stosowane tooVMs i wystąpienia ról na podstawie adresu MAC. Stan Hello te reguły są gromadzone co 60 sekund.
* **Licznik reguł:** zawiera wpisy dla ile razy każda grupa NSG do reguły jest stosowane toodeny lub zezwolić na ruch.

> [!NOTE]
> Dzienniki diagnostyczne są dostępne tylko dla grup NSG wdrożone za pośrednictwem modelu wdrażania usługi Azure Resource Manager hello. Nie można włączyć rejestrowania diagnostycznego w celu grup NSG wdrożone za pośrednictwem hello klasycznego modelu wdrażania. W celu lepszego zrozumienia hello dwóch modeli, odwołanie hello [modele wdrażania Azure opis](../resource-manager-deployment-model.md) artykułu.

Rejestrowanie aktywności (wcześniej znane jako inspekcji lub operacyjne dzienniki) jest domyślnie włączone dla grup NSG, został utworzony za pomocą obu modelu wdrożenia usługi Azure. toodetermine, jakie operacje zostały zakończone na grup NSG w hello dziennik aktywności, Wyszukaj wpisy zawierające hello następujące typy zasobów: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Witaj odczytu [omówienie hello dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn artykułu więcej o Dzienniki aktywności. 

## <a name="enable-diagnostic-logging"></a>Włączanie rejestrowania diagnostycznego

Należy włączyć rejestrowanie diagnostyczne *każdego* NSG ma toocollect danych. Witaj [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) wyjaśniono wysyłania dzienników diagnostycznych. Jeśli nie masz istniejącej grupy NSG, pełną hello etapami hello [Utwórz grupę zabezpieczeń sieci](virtual-networks-create-nsg-arm-pportal.md) toocreate artykułu, jeden. Można włączyć NSG przy użyciu dowolnej z następujących metod hello diagnostyczne:

### <a name="azure-portal"></a>Azure Portal

toouse hello portalu tooenable rejestrowania, logowanie toohello [portal](https://portal.azure.com). Kliknij przycisk **więcej usług**, wpisz *sieciowej grupy zabezpieczeń*. Wybierz hello NSG ma tooenable rejestrowania. Wykonaj instrukcje hello zasobów z systemem innym niż obliczeń w hello [Włączanie dzienników diagnostycznych w portalu hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu. Wybierz **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, lub oba rodzaje dzienników.

### <a name="powershell"></a>PowerShell

toouse tooenable PowerShell rejestrowanie, wykonaj te instrukcje hello hello [Włączanie dzienników diagnostycznych za pomocą programu PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu. Sprawdź następujące informacje przed wprowadzeniem polecenie z artykułu hello hello:

- Można określić hello toouse wartość dla hello `-ResourceId` parametru zastępując powitania po [tekst], zgodnie z potrzebami, następnie wpisując polecenie hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. Hello identyfikator dane wyjściowe polecenia hello wygląda podobnie zbyt*/subscriptions/ [Nazwa subskrypcji Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Tylko dane toocollect z kategorii dziennika należy dodać `-Categories [category]` toohello koniec polecenia hello w artykule hello, gdzie kategorii jest *NetworkSecurityGroupEvent* lub *NetworkSecurityGroupRuleCounter*. Jeśli nie używasz hello `-Categories` parametru, zbierania danych jest włączona dla dziennika kategorii.

### <a name="azure-command-line-interface-cli"></a>Azure interfejsu wiersza polecenia (CLI)

toouse hello rejestrowania tooenable interfejsu wiersza polecenia, wykonaj te instrukcje hello hello [Włączanie dzienników diagnostycznych za pomocą interfejsu wiersza polecenia](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artykułu. Sprawdź następujące informacje przed wprowadzeniem polecenie z artykułu hello hello:

- Można określić hello toouse wartość dla hello `-ResourceId` parametru zastępując powitania po [tekst], zgodnie z potrzebami, następnie wpisując polecenie hello `azure network nsg show [resource-group-name] [nsg-name]`. Hello identyfikator dane wyjściowe polecenia hello wygląda podobnie zbyt*/subscriptions/ [Nazwa subskrypcji Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Tylko dane toocollect z kategorii dziennika należy dodać `-Categories [category]` toohello koniec polecenia hello w artykule hello, gdzie kategorii jest *NetworkSecurityGroupEvent* lub *NetworkSecurityGroupRuleCounter*. Jeśli nie używasz hello `-Categories` parametru, zbierania danych jest włączona dla dziennika kategorii.

## <a name="logged-data"></a>Zarejestrowane dane

Dane w formacie JSON jest przeznaczony dla obu dzienników. określone dane Hello zapisywane dla każdego typu dziennika ma na liście hello następujące sekcje:

### <a name="event-log"></a>Dziennik zdarzeń
Ten dziennik zawiera informacje o NSG, które zasady są stosowane tooVMs i wystąpień roli usługi, na podstawie adresu MAC w chmurze. następujące przykładowe dane Hello jest rejestrowane dla każdego zdarzenia:

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a>Zasada dziennika liczników

Ten dziennik zawiera informacje o każdym tooresources reguły. Witaj przykład rejestrowane są następujące dane każdym razem, gdy reguła jest stosowana:

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a>Wyświetlanie i analizowanie dzienników

toolearn, w jaki sposób dane, rejestrować działania tooview odczytu hello [omówienie hello dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykułu. toolearn, jak dane, rejestrować Diagnostyka tooview odczytu hello [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykułu. Po wysłaniu diagnostyki danych tooLog Analytics można użyć hello [analytics sieciowej grupy zabezpieczeń usługi Azure](../log-analytics/log-analytics-azure-networking-analytics.md) rozszerzone szczegółowe informacje o rozwiązania do zarządzania (wersja zapoznawcza). 
