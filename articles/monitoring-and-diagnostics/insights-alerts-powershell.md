---
title: "Utwórz alerty dla usług Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Wyzwalacz wiadomości e-mail, powiadomienia, Wywołaj adresy URL witryny sieci Web (elementy webhook) lub automatyzacji po spełnieniu warunków, które określisz."
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
ms.openlocfilehash: d3fca8675c1f15b8fd0f952cfbf520f5c68478b3
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>W monitorze Azure tworzyć alerty metryki dla usługi Azure - PowerShell
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [Program PowerShell](insights-alerts-powershell.md)
> * [Interfejs wiersza polecenia](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Przegląd
W tym artykule przedstawiono sposób konfigurowania Azure metryki alertów za pomocą programu PowerShell.  

Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.

* **Wartości metryki** — uruchamia alert, gdy wartość określonej metryki przekracza próg przypisać w żadnym kierunku. Oznacza to, że oba wyzwala po spełnieniu warunku zostanie najpierw i następnie później podczas warunku jest już spełniane.    
* **Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia. Aby dowiedzieć się więcej o alertach dziennika aktywności [kliknij tutaj](monitoring-activity-log-alerts.md)

Można skonfigurować metryki alert do wyzwala, wykonaj następujące czynności:

* wysyłanie powiadomień e-mail do administratora usługi i współadministratorzy
* Wyślij wiadomość e-mail do dodatkowych wiadomości e-mail przez użytkownika.
* Wywołanie elementu webhook
* Uruchamia wykonywanie elementów runbook platformy Azure (tylko z portalu Azure)

Można skonfigurować i uzyskać informacje na temat przy użyciu reguły alertów

* [Azure portal](insights-alerts-portal.md)
* [Program PowerShell](insights-alerts-powershell.md)
* [Interfejs wiersza polecenia (CLI)](insights-alerts-command-line-interface.md)
* [Interfejs API REST Azure monitora](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Aby uzyskać dodatkowe informacje, zawsze można wpisać ```Get-Help``` , a następnie polecenie programu PowerShell chcesz uzyskać pomoc.

## <a name="create-alert-rules-in-powershell"></a>Tworzyć reguły alertów w programie PowerShell
1. Logowanie do platformy Azure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Pobranie listy subskrypcji posiadanego. Sprawdź, użytkownik pracuje z prawej subskrypcji. Jeśli nie, ustaw ją na właściwy przy użyciu dane wyjściowe z `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. Aby wyświetlić listę istniejących reguł dla grupy zasobów, użyj następującego polecenia:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. Aby utworzyć regułę, musisz mieć najpierw kilku ważnych informacji.

  * **Identyfikator zasobu** dla zasobu, aby ustawić alert dla
  * **Definicji metryk** dostępne dla tego zasobu

     Jednym ze sposobów Pobierz identyfikator zasobu jest korzystanie z portalu Azure. Zakładając, że zasób został już utworzony, wybierz go w portalu. Następnie w bloku dalej wybierz *właściwości* w obszarze *ustawienia* sekcji. **Identyfikator ZASOBU** jest polem w następnym bloku. Innym sposobem jest użycie [Eksploratora zasobów Azure](https://resources.azure.com/).

     Na przykład identyfikator zasobu dla aplikacji sieci web

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Można użyć `Get-AzureRmMetricDefinition` Aby wyświetlić listę wszystkich definicji metryki dla określonego zasobu.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Poniższy przykład generuje tabeli o nazwie metryki i jednostki dla tego metryki.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Pełną listę dostępnych opcji Get AzureRmMetricDefinition jest dostępna, uruchamiając `Get-Help Get-AzureRmMetricDefinition -Detailed`.
5. Poniższy przykład powoduje ustawienie alertu dla zasobu witryny sieci web. Wyzwalacze alertu zawsze, gdy odbierze spójnie cały ruch do 5 minut i ponownie po otrzymaniu żaden ruch na 5 minut.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. Aby utworzyć elementu webhook lub Wyślij wiadomość e-mail, gdy wyzwala alert, należy najpierw utworzyć wiadomości e-mail i/lub elementów webhook. Następnie od razu utworzyć regułę później znacznikiem akcje i jak pokazano w poniższym przykładzie. Nie można skojarzyć elementu webhook lub wiadomości e-mail przy użyciu reguły za pomocą programu PowerShell już utworzone.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. Aby sprawdzić, czy alerty zostały utworzone prawidłowo analizując poszczególnych reguł.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Usuń alerty. Te polecenia usuwania reguł utworzonych wcześniej w tym artykule.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Kolejne kroki
* [Omówienie monitorowania Azure](monitoring-overview.md) w tym typy informacji, można zbierać i monitorowania.
* Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).
* Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).
* Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).
* Pobierz [omówienie zbierania dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) zbierania szczegółowych o dużej częstotliwości metryk usługi.
* Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) się upewnić, że usługa jest dostępna i elastyczny.
