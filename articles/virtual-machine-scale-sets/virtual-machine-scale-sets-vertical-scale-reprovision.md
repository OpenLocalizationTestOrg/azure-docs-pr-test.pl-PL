---
title: zestawy skalowania maszyny wirtualnej platformy Azure skali aaaVertically | Dokumentacja firmy Microsoft
description: "Jak toovertically skalowania maszyny wirtualnej w odpowiedzi toomonitoring alertów z usługi Automatyzacja Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Pionowy automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej
W tym artykule opisano, jak toovertically skalować Azure [zestawy skalowania maszyny wirtualnej](https://azure.microsoft.com/services/virtual-machine-scale-sets/) z lub bez reprovisioning. Pionowy skalowania maszyn wirtualnych, które nie znajdują się w zestawy skalowania można znaleźć zbyt[skalowanie w pionie maszyny wirtualnej platformy Azure w usłudze Automatyzacja Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Skalować w pionie, znanej także jako *skalowanie w górę* i *dół*, oznacza zwiększenie lub zmniejszenie rozmiarów maszyn wirtualnych (VM) w odpowiedzi tooa obciążenia. Porównaj te z [skalowanie w poziomie](virtual-machine-scale-sets-autoscale-overview.md), nazywana także tooas *skalowanie w poziomie* i *skalować w*, gdzie hello liczbę maszyn wirtualnych jest zmianie w zależności od obciążenia hello.

Reprovisioning oznacza usunięcie istniejącej maszyny Wirtualnej i zastąpienie go innym. Zwiększenie lub zmniejszenie rozmiaru hello maszyn wirtualnych w zestawie skalowania maszyn wirtualnych, w niektórych przypadkach możesz mają tooresize istniejących maszyn wirtualnych i Zachowaj dane, a w innych przypadkach należy toodeploy nowych maszyn wirtualnych hello nowego rozmiaru. W tym dokumencie opisano w obu przypadkach.

Skalowanie w pionie mogą być przydatne podczas:

* Usługa oparta na maszynach wirtualnych jest wykorzystywane w obszarze (na przykład w weekendy). Zmniejszenie rozmiaru maszyny Wirtualnej hello można zmniejszyć koszty miesięcznych.
* Zwiększanie toocope rozmiar maszyny Wirtualnej z większą żądanie bez tworzenia dodatkowych maszyn wirtualnych.

Możesz skonfigurować pionowego skalowanie toobe wyzwalane na podstawie metryki na podstawie alertów z zestawu skali maszyny Wirtualnej. Po aktywowaniu hello alert go generowane elementu webhook tego wyzwalaczy, ustawione przez element runbook, które mogą być skalowane na skalę w górę lub w dół. Skalowanie w pionie można skonfigurować, wykonaj następujące czynności:

1. Utwórz konto usługi Automatyzacja Azure z funkcji Uruchom jako.
2. Importowanie elementów runbook skali pionowej automatyzacji Azure dla zestawy skalowania maszyny Wirtualnej w ramach subskrypcji.
3. Dodaj element tooyour elementu webhook.
4. Dodawanie alertu tooyour zestawu skali maszyny Wirtualnej za pomocą powiadomień elementu webhook.

> [!NOTE]
> Skalowanie w pionie automatyczne może nastąpić w określonym zakresie rozmiarów maszyn wirtualnych. Porównanie specyfikacji hello każdego rozmiaru przed podjęciem decyzji tooscale z jednego tooanother (większą liczbę nie zawsze wskazuje większy rozmiar maszyny Wirtualnej). Możesz wybrać tooscale między powitania po pary rozmiary:
> 
> | Rozmiary maszyn wirtualnych, skalowanie pary |  |
> | --- | --- |
> | Standardowa_A0 |Standardowa_A11 |
> | Standardowa_D1 |Standardowa_D14 |
> | Standardowa_DS1 |Standardowa_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standardowa_G1 |Standard_G5 |
> | Standardowa_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Utwórz konto usługi Automatyzacja Azure z funkcji Uruchom jako
najpierw Hello należy toodo jest utworzyć konto usługi Automatyzacja Azure, które będą obsługiwać wystąpienia zestawu skali maszyny Wirtualnej hello tooscale elementów runbook używane hello. Ostatnio [usługi Automatyzacja Azure](https://azure.microsoft.com/services/automation/) wprowadzone "Konto Uruchom jako" Funkcja hello, co sprawia, że skonfigurowanie hello nazwy głównej usługi dla automatycznie uruchomione hello elementy runbook w imieniu użytkownika bardzo proste. Możesz przeczytać dodatkowe informacje w artykule hello poniżej:

* [Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importowanie elementów runbook skali pionowej automatyzacji Azure w ramach subskrypcji
elementy runbook Hello potrzebne Skaluj toovertically Twojego zestawy skalowania maszyny Wirtualnej zostały już opublikowane w hello galerię elementów Runbook automatyzacji Azure. kroki tooimport hello postępuj zgodnie z ich do subskrypcji w tym artykule:

* [Galeria elementów Runbook i modułów dla usługi Automatyzacja Azure](../automation/automation-runbook-gallery.md)

Wybierz opcję Przeglądaj galerii hello z menu elementów Runbook hello:

![Toobe elementy Runbook zaimportowane][runbooks]

Hello elementów runbook, które należy zaimportować toobe są wyświetlane. Wybierz runbook hello oparte na czy ma pionowego, skalowania z lub bez reprovisioning:

![Galeria elementów Runbook][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Dodaj element tooyour elementu webhook
Po zaimportowaniu elementów runbook hello należy tooadd webhook toohello runbook, mogą być wyzwalane przez alert z zestawu skali maszyny Wirtualnej. w tym artykule opisano szczegóły Hello tworzenia elementu webhook dla elementu Runbook:

* [Azure automatyzacji elementów webhook](../automation/automation-webhooks.md)

> [!NOTE]
> Upewnij się, że kopiowania elementu webhook hello URI przed zamknięciem okna dialogowego elementu webhook hello ponieważ będzie on potrzebny w następnej sekcji hello.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Dodawanie alertu tooyour zestawu skali maszyny Wirtualnej
Poniżej przedstawiono sposób która zawiera skrypt programu PowerShell tooadd alertu tooa zestawu skali maszyny Wirtualnej. Można znaleźć toohello po tooget hello nazwa alertu hello metryki toofire hello: [metryki wspólnej Skalowanie automatyczne Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> Jest zalecana tooconfigure okna rozsądnym czasie hello alertu w kolejności tooavoid wyzwalania, skalowanie w pionie, wraz ze wszystkimi skojarzonymi przerw w obsłudze, zbyt często. Należy wziąć pod uwagę okna o co najmniej 20-30 minut lub dłużej. Należy wziąć pod uwagę poziomy skalowania, jeśli potrzebujesz tooavoid przerw w działaniu.
> 
> 

Aby uzyskać więcej informacji dotyczących sposobu toocreate alerty można znaleźć toohello następujące artykuły:

* [Przykładów dla platformy Azure Monitor PowerShell szybki start](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Przykładów dla platformy Azure CLI wieloplatformowych Monitor szybki start](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>Podsumowanie
W tym artykule pokazano proste przykłady skalowania pionowej. Te bloki konstrukcyjne — konto automatyzacji, elementy runbook, elementów webhook, alerty — może się łączyć szeroki zakres zdarzeń dostosowany zbiór akcji.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
