---
title: Skalowanie w pionie zestawy skalowania maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Sposób pionowo skalowania maszyny wirtualnej w odpowiedzi na monitorowanie alertów w usłudze Automatyzacja Azure"
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
ms.openlocfilehash: 9159a5a9041864fe06785829121233379c46bb03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="12f9b-103">Pionowy automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="12f9b-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="12f9b-104">W tym artykule opisano sposób skalowanie w pionie Azure [zestawy skalowania maszyny wirtualnej](https://azure.microsoft.com/services/virtual-machine-scale-sets/) z lub bez reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="12f9b-104">This article describes how to vertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="12f9b-105">Pionowy skalowania maszyn wirtualnych, które nie znajdują się w zestawy skalowania można znaleźć w temacie [skalowanie w pionie maszyny wirtualnej platformy Azure w usłudze Automatyzacja Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="12f9b-105">For vertical scaling of VMs which are not in scale sets, refer to [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="12f9b-106">Skalować w pionie, znanej także jako *skalowanie w górę* i *dół*, oznacza zwiększenie lub zmniejszenie rozmiarów maszyn wirtualnych (VM) w odpowiedzi na obciążenie.</span><span class="sxs-lookup"><span data-stu-id="12f9b-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response to a workload.</span></span> <span data-ttu-id="12f9b-107">Porównaj te z [skalowanie w poziomie](virtual-machine-scale-sets-autoscale-overview.md), nazywany również *skalowanie w poziomie* i *skalować w*, gdzie liczby maszyn wirtualnych jest zmianie w zależności od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="12f9b-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred to as *scale out* and *scale in*, where the number of VMs is altered depending on the workload.</span></span>

<span data-ttu-id="12f9b-108">Reprovisioning oznacza usunięcie istniejącej maszyny Wirtualnej i zastąpienie go innym.</span><span class="sxs-lookup"><span data-stu-id="12f9b-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="12f9b-109">Zwiększyć lub zmniejszyć rozmiar maszyn wirtualnych w zestawie skalowania maszyn wirtualnych, w niektórych przypadkach chcesz zmienić rozmiar istniejących maszyn wirtualnych i Zachowaj dane, a w innych przypadkach należy wdrożyć nowe maszyny wirtualne o nowy rozmiar.</span><span class="sxs-lookup"><span data-stu-id="12f9b-109">When you increase or decrease the size of VMs in a VM Scale Set, in some cases you want to resize existing VMs and retain your data, while in other cases you need to deploy new VMs of the new size.</span></span> <span data-ttu-id="12f9b-110">W tym dokumencie opisano w obu przypadkach.</span><span class="sxs-lookup"><span data-stu-id="12f9b-110">This document covers both cases.</span></span>

<span data-ttu-id="12f9b-111">Skalowanie w pionie mogą być przydatne podczas:</span><span class="sxs-lookup"><span data-stu-id="12f9b-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="12f9b-112">Usługa oparta na maszynach wirtualnych jest wykorzystywane w obszarze (na przykład w weekendy).</span><span class="sxs-lookup"><span data-stu-id="12f9b-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="12f9b-113">Zmniejszenie rozmiaru maszyny Wirtualnej można zmniejszyć koszty miesięcznych.</span><span class="sxs-lookup"><span data-stu-id="12f9b-113">Reducing the VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="12f9b-114">Zwiększanie rozmiaru maszyny Wirtualnej, aby poradzić sobie z większą żądanie bez tworzenia dodatkowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="12f9b-114">Increasing VM size to cope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="12f9b-115">Można skonfigurować skalowanie w pionie być wyzwalane na podstawie alertów według metryki z zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12f9b-115">You can set up vertical scaling to be triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="12f9b-116">Gdy alert jest aktywny go generowane elementu webhook tego wyzwalaczy, ustawione przez element runbook, które mogą być skalowane na skalę w górę lub w dół.</span><span class="sxs-lookup"><span data-stu-id="12f9b-116">When the alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="12f9b-117">Skalowanie w pionie można skonfigurować, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="12f9b-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="12f9b-118">Utwórz konto usługi Automatyzacja Azure z funkcji Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="12f9b-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="12f9b-119">Importowanie elementów runbook skali pionowej automatyzacji Azure dla zestawy skalowania maszyny Wirtualnej w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="12f9b-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="12f9b-120">Dodawanie elementu webhook do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="12f9b-120">Add a webhook to your runbook.</span></span>
4. <span data-ttu-id="12f9b-121">Dodaj alert do sieci zestawu skali maszyny Wirtualnej za pomocą powiadomień elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="12f9b-121">Add an alert to your VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="12f9b-122">Skalowanie w pionie automatyczne może nastąpić w określonym zakresie rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="12f9b-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="12f9b-123">Porównanie specyfikacji każdego rozmiaru przed podjęciem decyzji o skali: od jednej do innego (większą liczbę nie zawsze wskazuje większy rozmiar maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="12f9b-123">Compare the specifications of each size before deciding to scale from one to another (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="12f9b-124">Możesz skalować między parami następujących rozmiarów:</span><span class="sxs-lookup"><span data-stu-id="12f9b-124">You can choose to scale between the following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="12f9b-125">Rozmiary maszyn wirtualnych, skalowanie pary</span><span class="sxs-lookup"><span data-stu-id="12f9b-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="12f9b-126">Standardowa_A0</span><span class="sxs-lookup"><span data-stu-id="12f9b-126">Standard_A0</span></span> |<span data-ttu-id="12f9b-127">Standardowa_A11</span><span class="sxs-lookup"><span data-stu-id="12f9b-127">Standard_A11</span></span> |
> | <span data-ttu-id="12f9b-128">Standardowa_D1</span><span class="sxs-lookup"><span data-stu-id="12f9b-128">Standard_D1</span></span> |<span data-ttu-id="12f9b-129">Standardowa_D14</span><span class="sxs-lookup"><span data-stu-id="12f9b-129">Standard_D14</span></span> |
> | <span data-ttu-id="12f9b-130">Standardowa_DS1</span><span class="sxs-lookup"><span data-stu-id="12f9b-130">Standard_DS1</span></span> |<span data-ttu-id="12f9b-131">Standardowa_DS14</span><span class="sxs-lookup"><span data-stu-id="12f9b-131">Standard_DS14</span></span> |
> | <span data-ttu-id="12f9b-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="12f9b-132">Standard_D1v2</span></span> |<span data-ttu-id="12f9b-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="12f9b-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="12f9b-134">Standardowa_G1</span><span class="sxs-lookup"><span data-stu-id="12f9b-134">Standard_G1</span></span> |<span data-ttu-id="12f9b-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="12f9b-135">Standard_G5</span></span> |
> | <span data-ttu-id="12f9b-136">Standardowa_GS1</span><span class="sxs-lookup"><span data-stu-id="12f9b-136">Standard_GS1</span></span> |<span data-ttu-id="12f9b-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="12f9b-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="12f9b-138">Utwórz konto usługi Automatyzacja Azure z funkcji Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="12f9b-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="12f9b-139">W pierwszej kolejności należy wykonać to utworzyć konto usługi Automatyzacja Azure, które będą obsługiwać elementów runbook, używana do skalowania wystąpienia zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12f9b-139">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="12f9b-140">Ostatnio [usługi Automatyzacja Azure](https://azure.microsoft.com/services/automation/) wprowadzono funkcję "Konto Uruchom jako", co sprawia, że ustawienia zapasowej główną usługi dla automatycznie uruchomione elementy runbook w imieniu użytkownika bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="12f9b-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="12f9b-141">Możesz przeczytać więcej na temat tego artykułu poniżej:</span><span class="sxs-lookup"><span data-stu-id="12f9b-141">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="12f9b-142">Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure</span><span class="sxs-lookup"><span data-stu-id="12f9b-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="12f9b-143">Importowanie elementów runbook skali pionowej automatyzacji Azure w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="12f9b-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="12f9b-144">Elementy runbook, konieczne jest skalowanie w pionie z zestawy skalowania maszyny Wirtualnej zostały już opublikowane w galerii elementu Runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="12f9b-144">The runbooks needed to vertically scale your VM Scale Sets are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="12f9b-145">Aby zaimportować je do subskrypcji wykonaj kroki opisane w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="12f9b-145">To import them into your subscription follow the steps in this article:</span></span>

* [<span data-ttu-id="12f9b-146">Galeria elementów Runbook i modułów dla usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="12f9b-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="12f9b-147">Wybierz opcję Galerii przeglądania z menu elementów Runbook:</span><span class="sxs-lookup"><span data-stu-id="12f9b-147">Choose the Browse Gallery option from the Runbooks menu:</span></span>

![Elementy Runbook do zaimportowania][runbooks]

<span data-ttu-id="12f9b-149">Wyświetlane są elementy runbook, które muszą zostać zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="12f9b-149">The runbooks that need to be imported are shown.</span></span> <span data-ttu-id="12f9b-150">Wybierz element runbook, czy ma pionowego, skalowania z lub bez reprovisioning — na podstawie:</span><span class="sxs-lookup"><span data-stu-id="12f9b-150">Select the runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Galeria elementów Runbook][gallery]

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="12f9b-152">Dodawanie elementu webhook z elementem runbook</span><span class="sxs-lookup"><span data-stu-id="12f9b-152">Add a webhook to your runbook</span></span>
<span data-ttu-id="12f9b-153">Po zaimportowaniu elementów runbook, które będą potrzebne, aby dodać elementu webhook do elementu runbook, mogą być wyzwalane przez alert z zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12f9b-153">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="12f9b-154">W tym artykule opisano szczegółów tworzenia elementu webhook dla elementu Runbook:</span><span class="sxs-lookup"><span data-stu-id="12f9b-154">The details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="12f9b-155">Azure automatyzacji elementów webhook</span><span class="sxs-lookup"><span data-stu-id="12f9b-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="12f9b-156">Upewnij się, że należy skopiować identyfikator URI elementu webhook przed zamknięciem okna dialogowego elementu webhook, ponieważ będzie on potrzebny w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="12f9b-156">Make sure you copy the webhook URI before closing the webhook dialog as you will need this in the next section.</span></span>
> 
> 

## <a name="add-an-alert-to-your-vm-scale-set"></a><span data-ttu-id="12f9b-157">Dodaj alert do zestawu skali maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="12f9b-157">Add an alert to your VM Scale Set</span></span>
<span data-ttu-id="12f9b-158">Poniżej znajduje się skrypt programu PowerShell, który pokazuje, jak dodać alert do zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12f9b-158">Below is a PowerShell script which shows how to add an alert to a VM Scale Set.</span></span> <span data-ttu-id="12f9b-159">Zapoznaj się z artykułem następujące nazwy metryki wyzwalać alert na: [metryki wspólnej Skalowanie automatyczne Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="12f9b-159">Refer to the following article to get the name of the metric to fire the alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="12f9b-160">Zalecane jest, aby skonfigurować okno czasu alertu, aby uniknąć wyzwalania skalowanie w pionie i wszystkie skojarzone przerw w obsłudze, zbyt często.</span><span class="sxs-lookup"><span data-stu-id="12f9b-160">It is recommended to configure a reasonable time window for the alert in order to avoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="12f9b-161">Należy wziąć pod uwagę okna o co najmniej 20-30 minut lub dłużej.</span><span class="sxs-lookup"><span data-stu-id="12f9b-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="12f9b-162">Należy wziąć pod uwagę skalowanie, aby uniknąć przerw w poziomie.</span><span class="sxs-lookup"><span data-stu-id="12f9b-162">Consider horizontal scaling if you need to avoid any interruption.</span></span>
> 
> 

<span data-ttu-id="12f9b-163">Aby uzyskać więcej informacji na temat tworzenia alertów można znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="12f9b-163">For more information on how to create alerts refer to the following articles:</span></span>

* [<span data-ttu-id="12f9b-164">Przykładów dla platformy Azure Monitor PowerShell szybki start</span><span class="sxs-lookup"><span data-stu-id="12f9b-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="12f9b-165">Przykładów dla platformy Azure CLI wieloplatformowych Monitor szybki start</span><span class="sxs-lookup"><span data-stu-id="12f9b-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="12f9b-166">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="12f9b-166">Summary</span></span>
<span data-ttu-id="12f9b-167">W tym artykule pokazano proste przykłady skalowania pionowej.</span><span class="sxs-lookup"><span data-stu-id="12f9b-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="12f9b-168">Te bloki konstrukcyjne — konto automatyzacji, elementy runbook, elementów webhook, alerty — może się łączyć szeroki zakres zdarzeń dostosowany zbiór akcji.</span><span class="sxs-lookup"><span data-stu-id="12f9b-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
