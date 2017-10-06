---
title: "aaaAzure rozwiązania analizy sieci w Log Analytics | Dokumentacja firmy Microsoft"
description: "Możesz użyć hello rozwiązania Azure Networking analizy dzienników grupy zabezpieczeń sieci platformy Azure tooreview analizy dzienników i dzienniki bramy aplikacji Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Sieć platformy Azure monitorowanie rozwiązań w analizy dzienników

Analiza dzienników oferuje hello następujące rozwiązania do monitorowania sieci:
* Monitor wydajności sieci (NPM) do
 * Monitorowanie kondycji hello sieci
* Azure tooreview analytics bramy aplikacji
 * Dzienniki bramy aplikacji Azure
 * Azure metryki bramy aplikacji
* Grupy zabezpieczeń sieci Azure tooreview analityka
 * Dzienniki grupy zabezpieczeń sieci platformy Azure

## <a name="network-performance-monitor-npm"></a>Monitor wydajności sieci (NPM)

Witaj [monitora wydajności sieci](log-analytics-network-performance-monitor.md) rozwiązanie do zarządzania jest rozwiązanie, monitoruje kondycję hello, dostępności i uzyskiwanie sieci do monitorowania sieci.  Jest używana toomonitor łączność między:

* Chmura publiczna i lokalnych
* centra danych i lokalizacje użytkownika (biurach oddziałów)
* podsieci hosting różnych warstw aplikacji wielowarstwowych.

Aby uzyskać więcej informacji, zobacz [monitora wydajności sieci](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure analytics bramy aplikacji i grupy zabezpieczeń sieci
toouse hello rozwiązania:
1. Dodaj tooLog rozwiązania zarządzania hello Analytics, a
2. Włącz diagnostykę toodirect hello diagnostyki tooa analizy dzienników z obszaru roboczego. Nie jest magazynu obiektów Blob tooAzure niezbędne toowrite hello dzienników.

Można włączyć diagnostyki i hello odpowiednie rozwiązanie dla jednej lub obu z bramy aplikacji i grup zabezpieczeń sieci.

Jeśli nie włączaj rejestrowania diagnostyki dla określonego typu zasobu, ale zainstalować rozwiązanie hello hello bloków pulpitu nawigacyjnego dla tego zasobu są puste i wyświetlony komunikat o błędzie.

> [!NOTE]
> W stycznia 2017 r. hello obsługiwane sposób wysyłania dzienników z bramy aplikacji i grup zabezpieczeń sieci tooLog zmienić Analytics. Jeśli widzisz hello **Analytics sieci Azure (przestarzałe)** rozwiązania, odwoływać się za[migracja z rozwiązania do analizy sieci starego hello](#migrating-from-the-old-networking-analytics-solution) czynności należy toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Przejrzyj szczegóły zbierania danych w sieci Azure
Hello Azure Application Gateway analizy i rozwiązania do zarządzania analytics hello sieciowej grupy zabezpieczeń zbierania dzienników diagnostycznych bezpośrednio z bramy aplikacji Azure i grup zabezpieczeń sieci. Nie jest konieczne toowrite hello dzienniki tooAzure magazynu obiektów Blob i agent nie jest wymagany do zbierania danych.

Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla analizy brama aplikacji w usłudze Azure i hello analytics grupy zabezpieczeń sieci.

| Platforma | Bezpośrednie agenta | Agent menedżera operacji centrum systemów | Azure | Wymagane programu Operations Manager? | Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania | Częstotliwość zbierania |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |Podczas rejestrowania |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Azure rozwiązania analizy brama aplikacji w analizy dzienników

![Azure symbol analizy bramy aplikacji](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

powitania po dzienniki są obsługiwane w przypadku bram aplikacji:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

następujące metryki Hello są obsługiwane w przypadku bram aplikacji:

* Przepływność 5 minut

### <a name="install-and-configure-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj hello następujące instrukcje tooinstall i skonfiguruj rozwiązania analizy hello Azure Application Gateway:

1. Włącz hello rozwiązania analizy bramy aplikacji Azure z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. Włączanie rejestrowania diagnostyki dla hello [bramy aplikacji](../application-gateway/application-gateway-diagnostics.md) ma toomonitor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Włącz diagnostykę bramy aplikacji Azure w portalu hello

1. W hello portalu Azure Przejdź toomonitor zasobów bramy aplikacji toohello
2. Wybierz *dzienników diagnostycznych* hello tooopen po stronie

   ![obraz zasobu bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Kliknij przycisk *Włącz diagnostykę* hello tooopen po stronie

   ![obraz zasobu bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. Kliknij tooturn diagnostykę, *na* w obszarze *stanu*
5. Kliknij przycisk wyboru hello *wysyłania tooLog analityka*
6. Wybierz istniejący obszar roboczy analizy dzienników lub tworzenie obszaru roboczego
7. Kliknij przycisk wyboru hello **dziennika** dla każdego toocollect typy dziennika hello
8. Kliknij przycisk *zapisać* tooenable hello rejestrowania diagnostyki tooLog analityka

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Włącz diagnostykę sieci platformy Azure przy użyciu programu PowerShell

Witaj następującego skryptu programu PowerShell zawiera przykładowy sposób tooenable diagnostyczne dla bramy aplikacji.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Użyj analizy bramy aplikacji Azure
![Obraz kafelka analytics bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Po kliknięciu hello **analytics Azure Application Gateway** kafelka na powitania omówienie wyświetlanie podsumowań dzienników i następnie przejść do szczegółów w toodetails dla hello następujące kategorie:

* Rejestruje dostęp do bramy aplikacji
  * Błędy na kliencie i serwerze dla dzienników dostępu bramy aplikacji
  * Liczba żądań na godzinę dla każdej bramy aplikacji
  * Nieudane żądania na godzinę dla każdej bramy aplikacji
  * Błędy przez agenta użytkownika dla bramy aplikacji
* Wydajność bramy aplikacji
  * Kondycja hosta bramy aplikacji
  * Maksymalne i 95 percentyl żądań bramy aplikacji nie powiodło się

![Obraz pulpitu nawigacyjnego analytics bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Obraz pulpitu nawigacyjnego analytics bramy aplikacji Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

Na powitania **analytics Azure Application Gateway** pulpitu nawigacyjnego, przejrzyj hello informacje podsumowania w jednym z bloków hello, a następnie kliknij jedną tooview szczegółowe informacje dotyczące hello dziennik wyszukiwania strony.

Na wszystkich stronach wyszukiwania dziennika hello można wyświetlić wyniki według czasu, szczegółowe wyniki i historię dziennik wyszukiwania. Można również filtrować według aspekty toonarrow hello wyników.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Grupy zabezpieczeń sieci Azure rozwiązania analizy w analizy dzienników

![Symbol Analytics sieciowej grupy zabezpieczeń usługi Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

powitania po dzienniki są obsługiwane w przypadku grup zabezpieczeń sieci:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj hello następujące instrukcje tooinstall i skonfiguruj rozwiązania Azure Networking analizy hello:

1. Włącz hello rozwiązania analizy Azure sieciową grupę zabezpieczeń z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. Włączanie rejestrowania diagnostyki dla hello [sieciowej grupy zabezpieczeń](../virtual-network/virtual-network-nsg-manage-log.md) zasoby, które chcesz toomonitor.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Włącz diagnostykę grupy zabezpieczeń sieci platformy Azure w portalu hello

1. W hello portalu Azure Przejdź toohello sieciowej grupy zabezpieczeń zasobów toomonitor
2. Wybierz *dzienników diagnostycznych* hello tooopen po stronie

   ![Obraz zasobów Azure sieciowej grupy zabezpieczeń](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Kliknij przycisk *Włącz diagnostykę* hello tooopen po stronie

   ![Obraz zasobów Azure sieciowej grupy zabezpieczeń](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. Kliknij tooturn diagnostykę, *na* w obszarze *stanu*
5. Kliknij przycisk wyboru hello *wysyłania tooLog analityka*
6. Wybierz istniejący obszar roboczy analizy dzienników lub tworzenie obszaru roboczego
7. Kliknij przycisk wyboru hello **dziennika** dla każdego toocollect typy dziennika hello
8. Kliknij przycisk *zapisać* tooenable hello rejestrowania diagnostyki tooLog analityka

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Włącz diagnostykę sieci platformy Azure przy użyciu programu PowerShell

Witaj następującego skryptu programu PowerShell zawiera przykładowy sposób tooenable diagnostyczne dla grup zabezpieczeń sieci
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Użyj grupy zabezpieczeń sieci Azure analityka
Po kliknięciu hello **analytics sieciowej grupy zabezpieczeń usługi Azure** kafelka na powitania omówienie wyświetlanie podsumowań dzienników i następnie przejść do szczegółów w toodetails dla hello następujące kategorie:

* Grupy zabezpieczeń sieci zablokowane przepływów
  * Reguły grupy zabezpieczeń sieci z przepływami zablokowanych
  * Adresy MAC z przepływami zablokowanych
* Dozwolone przepływów grupy zabezpieczeń sieci
  * Reguły grupy zabezpieczeń sieci z przepływami dozwolone
  * Adresy MAC z przepływami dozwolone

![Obraz pulpitu nawigacyjnego analytics sieciowej grupy zabezpieczeń usługi Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Obraz pulpitu nawigacyjnego analytics sieciowej grupy zabezpieczeń usługi Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

Na powitania **analytics sieciowej grupy zabezpieczeń usługi Azure** pulpitu nawigacyjnego, przejrzyj hello informacje podsumowania w jednym z bloków hello, a następnie kliknij jedną tooview szczegółowe informacje dotyczące hello dziennik wyszukiwania strony.

Na wszystkich stronach wyszukiwania dziennika hello można wyświetlić wyniki według czasu, szczegółowe wyniki i historię dziennik wyszukiwania. Można również filtrować według aspekty toonarrow hello wyników.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Migracja z rozwiązania do analizy sieci starego hello
W stycznia 2017 r. hello obsługiwane sposób wysyłania dzienników z bramy aplikacji Azure i grup zabezpieczeń sieci Azure tooLog zmienić Analytics. Te zmiany zapewniają hello następujące korzyści:
+ Dzienniki są zapisywane bezpośrednio tooLog Analytics bez hello muszą toouse konta magazynu
+ Mniejsze opóźnienia od czasu hello, kiedy są dzienniki generowane toothem dostępne w analizy dzienników
+ Mniejszej liczby kroków konfiguracji
+ Format wspólne dla wszystkich typów Diagnostyka Azure

Witaj toouse aktualizacja rozwiązań:

1. [Skonfiguruj toobe diagnostyki wysyłane bezpośrednio tooLog Analytics z bramy aplikacji Azure](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Skonfiguruj toobe diagnostyki wysyłane bezpośrednio tooLog Analytics z grup zabezpieczeń sieci platformy Azure](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Włącz hello *analizy bramy aplikacji Azure* i hello *analiza grupy zabezpieczeń sieci Azure* rozwiązania za pomocą hello procesu opisanego w [rozwiązań dodać analizy dzienników Witaj galerii rozwiązań](log-analytics-add-solutions.md)
3. Wszystkie zapisane kwerendy, pulpity nawigacyjne lub alerty toouse hello nowy typ danych
  + Typ jest tooAzureDiagnostics. Można użyć dzienników sieci toofilter tooAzure hello typu zasobu.

    | Zamiast: | Za pomocą: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Dla dowolnego pola, które sufiks \_s, \_d, lub \_g w nazwie hello, zmień hello pierwszy znak toolower przypadku
   + Dla dowolnego pola, które sufiks \_o w polu Nazwa danych hello jest podzielony na poszczególnych pól na podstawie nazw pól hello zagnieżdżone.
4. Usuń hello *Azure Networking Analytics (przestarzały)* rozwiązania.
  + Jeśli używasz programu PowerShell, użyj`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

Dane zbierane przed hello zmiany nie jest widoczna w hello nowego rozwiązania. Możesz kontynuować tooquery dla tego danych przy użyciu hello stary typ i nazwy pola.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Następne kroki
* Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane diagnostyczne platformy Azure.
