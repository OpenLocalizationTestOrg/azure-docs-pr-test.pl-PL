---
title: "alerty aaaCreate dla usług Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Gdy są spełnione warunki hello wyzwolenia wiadomości e-mail, powiadomienia, adresy URL witryny sieci Web wywołania (elementy webhook) lub automatyzacji."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>W monitorze Azure tworzyć alerty metryki dla usługi Azure - PowerShell
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [Program PowerShell](insights-alerts-powershell.md)
> * [Interfejs wiersza polecenia](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak tooset zapasowej Azure Metryka alerty za pomocą programu PowerShell.  

Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.

* **Wartości metryki** — Witaj alertu wyzwalacze, jeśli wartość hello określonej metryki przecina próg przypisać w żadnym kierunku. Oznacza to, że oba wyzwala kiedy najpierw zostanie spełniony warunek hello i następnie później podczas warunku jest już spełniane.    
* **Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia. więcej informacji na temat alertów dotyczących działań w dzienniku toolearn [kliknij tutaj](monitoring-activity-log-alerts.md)

Można skonfigurować hello metryki toodo alertów po, wyzwala:

* Wyślij administratora usługi toohello powiadomienia e-mail i współadministratorzy
* Wyślij wiadomość e-mail tooadditional wiadomości e-mail, które określisz.
* Wywołanie elementu webhook
* Uruchamia wykonywanie elementów runbook platformy Azure (tylko z hello portalu Azure)

Można skonfigurować i uzyskać informacje na temat przy użyciu reguły alertów

* [Witryna Azure Portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [Interfejs wiersza polecenia (CLI)](insights-alerts-command-line-interface.md)
* [Interfejs API REST Azure monitora](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Aby uzyskać dodatkowe informacje, zawsze można wpisać ```Get-Help``` , a następnie hello polecenia programu PowerShell, które chcesz uzyskać pomoc.

## <a name="create-alert-rules-in-powershell"></a>Tworzyć reguły alertów w programie PowerShell
1. Zaloguj się za tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Pobranie listy subskrypcji powitania od posiadanego. Sprawdź, użytkownik pracuje z subskrypcją prawo hello. Jeśli nie, ustaw prawo toohello jeden przy użyciu dane wyjściowe hello `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. toolist istniejących reguł dla grupy zasobów, hello Użyj następującego polecenia:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate regułę, należy toohave kilku ważnych informacji najpierw.

  * Witaj **identyfikator zasobu** hello zasobu ma tooset alert dla
  * Witaj **definicji metryk** dostępne dla tego zasobu

     Jednym ze sposobów tooget hello identyfikator zasobu jest hello toouse portalu Azure. Zakładając, że zasób hello został już utworzony, wybierz go w portalu hello. Następnie w bloku dalej hello, wybierz *właściwości* w obszarze hello *ustawienia* sekcji. **Identyfikator ZASOBU** jest polem w następnym bloku hello. Innym sposobem jest toouse hello [Eksploratora zasobów Azure](https://resources.azure.com/).

     Na przykład identyfikator zasobu dla aplikacji sieci web

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Można użyć `Get-AzureRmMetricDefinition` tooview hello lista wszystkie definicje metryk dla określonego zasobu.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Witaj poniższy przykład generuje tabeli z metryką hello nazwy i hello jednostki dla tego metryki.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Pełną listę dostępnych opcji Get AzureRmMetricDefinition jest dostępna, uruchamiając polecenie Get-MetricDefinitions.
5. powitania po przykład konfiguruje alert o zasobów witryny sieci web. Wyzwalacze alertu Hello zawsze, gdy odbierze spójnie cały ruch do 5 minut i ponownie po otrzymaniu żaden ruch na 5 minut.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate elementu webhook lub wysyłania wiadomości e-mail podczas wyzwala alert, najpierw utworzyć hello poczty e-mail i/lub elementów webhook. Od razu utworzyć regułę hello później z hello - tag akcje i pokazane na powitania poniższy przykład. Nie można skojarzyć elementu webhook lub wiadomości e-mail przy użyciu reguły za pomocą programu PowerShell już utworzone.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify czy alerty zostały utworzone prawidłowo analizując hello poszczególnych reguł.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Usuń alerty. Te polecenia usuwania reguł hello utworzonej wcześniej w tym artykule.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Następne kroki
* [Omówienie monitorowania Azure](monitoring-overview.md) tym hello typy informacji, można zbierać i monitorowania.
* Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).
* Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).
* Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).
* Pobierz [omówienie zbierania dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) toocollect szczegółowe metryki wysokiej częstotliwości w usłudze.
* Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.
