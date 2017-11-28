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
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="4df24-103">Pionowy automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4df24-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="4df24-104">W tym artykule opisano, jak toovertically skalować Azure [zestawy skalowania maszyny wirtualnej](https://azure.microsoft.com/services/virtual-machine-scale-sets/) z lub bez reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="4df24-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="4df24-105">Pionowy skalowania maszyn wirtualnych, które nie znajdują się w zestawy skalowania można znaleźć zbyt[skalowanie w pionie maszyny wirtualnej platformy Azure w usłudze Automatyzacja Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4df24-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4df24-106">Skalować w pionie, znanej także jako *skalowanie w górę* i *dół*, oznacza zwiększenie lub zmniejszenie rozmiarów maszyn wirtualnych (VM) w odpowiedzi tooa obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4df24-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="4df24-107">Porównaj te z [skalowanie w poziomie](virtual-machine-scale-sets-autoscale-overview.md), nazywana także tooas *skalowanie w poziomie* i *skalować w*, gdzie hello liczbę maszyn wirtualnych jest zmianie w zależności od obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="4df24-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="4df24-108">Reprovisioning oznacza usunięcie istniejącej maszyny Wirtualnej i zastąpienie go innym.</span><span class="sxs-lookup"><span data-stu-id="4df24-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="4df24-109">Zwiększenie lub zmniejszenie rozmiaru hello maszyn wirtualnych w zestawie skalowania maszyn wirtualnych, w niektórych przypadkach możesz mają tooresize istniejących maszyn wirtualnych i Zachowaj dane, a w innych przypadkach należy toodeploy nowych maszyn wirtualnych hello nowego rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="4df24-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="4df24-110">W tym dokumencie opisano w obu przypadkach.</span><span class="sxs-lookup"><span data-stu-id="4df24-110">This document covers both cases.</span></span>

<span data-ttu-id="4df24-111">Skalowanie w pionie mogą być przydatne podczas:</span><span class="sxs-lookup"><span data-stu-id="4df24-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="4df24-112">Usługa oparta na maszynach wirtualnych jest wykorzystywane w obszarze (na przykład w weekendy).</span><span class="sxs-lookup"><span data-stu-id="4df24-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="4df24-113">Zmniejszenie rozmiaru maszyny Wirtualnej hello można zmniejszyć koszty miesięcznych.</span><span class="sxs-lookup"><span data-stu-id="4df24-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="4df24-114">Zwiększanie toocope rozmiar maszyny Wirtualnej z większą żądanie bez tworzenia dodatkowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4df24-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="4df24-115">Możesz skonfigurować pionowego skalowanie toobe wyzwalane na podstawie metryki na podstawie alertów z zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4df24-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="4df24-116">Po aktywowaniu hello alert go generowane elementu webhook tego wyzwalaczy, ustawione przez element runbook, które mogą być skalowane na skalę w górę lub w dół.</span><span class="sxs-lookup"><span data-stu-id="4df24-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="4df24-117">Skalowanie w pionie można skonfigurować, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4df24-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="4df24-118">Utwórz konto usługi Automatyzacja Azure z funkcji Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="4df24-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="4df24-119">Importowanie elementów runbook skali pionowej automatyzacji Azure dla zestawy skalowania maszyny Wirtualnej w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4df24-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="4df24-120">Dodaj element tooyour elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="4df24-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="4df24-121">Dodawanie alertu tooyour zestawu skali maszyny Wirtualnej za pomocą powiadomień elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="4df24-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="4df24-122">Skalowanie w pionie automatyczne może nastąpić w określonym zakresie rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4df24-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="4df24-123">Porównanie specyfikacji hello każdego rozmiaru przed podjęciem decyzji tooscale z jednego tooanother (większą liczbę nie zawsze wskazuje większy rozmiar maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="4df24-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="4df24-124">Możesz wybrać tooscale między powitania po pary rozmiary:</span><span class="sxs-lookup"><span data-stu-id="4df24-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="4df24-125">Rozmiary maszyn wirtualnych, skalowanie pary</span><span class="sxs-lookup"><span data-stu-id="4df24-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="4df24-126">Standardowa_A0</span><span class="sxs-lookup"><span data-stu-id="4df24-126">Standard_A0</span></span> |<span data-ttu-id="4df24-127">Standardowa_A11</span><span class="sxs-lookup"><span data-stu-id="4df24-127">Standard_A11</span></span> |
> | <span data-ttu-id="4df24-128">Standardowa_D1</span><span class="sxs-lookup"><span data-stu-id="4df24-128">Standard_D1</span></span> |<span data-ttu-id="4df24-129">Standardowa_D14</span><span class="sxs-lookup"><span data-stu-id="4df24-129">Standard_D14</span></span> |
> | <span data-ttu-id="4df24-130">Standardowa_DS1</span><span class="sxs-lookup"><span data-stu-id="4df24-130">Standard_DS1</span></span> |<span data-ttu-id="4df24-131">Standardowa_DS14</span><span class="sxs-lookup"><span data-stu-id="4df24-131">Standard_DS14</span></span> |
> | <span data-ttu-id="4df24-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="4df24-132">Standard_D1v2</span></span> |<span data-ttu-id="4df24-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="4df24-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="4df24-134">Standardowa_G1</span><span class="sxs-lookup"><span data-stu-id="4df24-134">Standard_G1</span></span> |<span data-ttu-id="4df24-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="4df24-135">Standard_G5</span></span> |
> | <span data-ttu-id="4df24-136">Standardowa_GS1</span><span class="sxs-lookup"><span data-stu-id="4df24-136">Standard_GS1</span></span> |<span data-ttu-id="4df24-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="4df24-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="4df24-138">Utwórz konto usługi Automatyzacja Azure z funkcji Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="4df24-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="4df24-139">najpierw Hello należy toodo jest utworzyć konto usługi Automatyzacja Azure, które będą obsługiwać wystąpienia zestawu skali maszyny Wirtualnej hello tooscale elementów runbook używane hello.</span><span class="sxs-lookup"><span data-stu-id="4df24-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="4df24-140">Ostatnio [usługi Automatyzacja Azure](https://azure.microsoft.com/services/automation/) wprowadzone "Konto Uruchom jako" Funkcja hello, co sprawia, że skonfigurowanie hello nazwy głównej usługi dla automatycznie uruchomione hello elementy runbook w imieniu użytkownika bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="4df24-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="4df24-141">Możesz przeczytać dodatkowe informacje w artykule hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="4df24-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="4df24-142">Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4df24-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="4df24-143">Importowanie elementów runbook skali pionowej automatyzacji Azure w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4df24-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="4df24-144">elementy runbook Hello potrzebne Skaluj toovertically Twojego zestawy skalowania maszyny Wirtualnej zostały już opublikowane w hello galerię elementów Runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="4df24-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="4df24-145">kroki tooimport hello postępuj zgodnie z ich do subskrypcji w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="4df24-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="4df24-146">Galeria elementów Runbook i modułów dla usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="4df24-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="4df24-147">Wybierz opcję Przeglądaj galerii hello z menu elementów Runbook hello:</span><span class="sxs-lookup"><span data-stu-id="4df24-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![Toobe elementy Runbook zaimportowane][runbooks]

<span data-ttu-id="4df24-149">Hello elementów runbook, które należy zaimportować toobe są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="4df24-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="4df24-150">Wybierz runbook hello oparte na czy ma pionowego, skalowania z lub bez reprovisioning:</span><span class="sxs-lookup"><span data-stu-id="4df24-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Galeria elementów Runbook][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="4df24-152">Dodaj element tooyour elementu webhook</span><span class="sxs-lookup"><span data-stu-id="4df24-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="4df24-153">Po zaimportowaniu elementów runbook hello należy tooadd webhook toohello runbook, mogą być wyzwalane przez alert z zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4df24-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="4df24-154">w tym artykule opisano szczegóły Hello tworzenia elementu webhook dla elementu Runbook:</span><span class="sxs-lookup"><span data-stu-id="4df24-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="4df24-155">Azure automatyzacji elementów webhook</span><span class="sxs-lookup"><span data-stu-id="4df24-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="4df24-156">Upewnij się, że kopiowania elementu webhook hello URI przed zamknięciem okna dialogowego elementu webhook hello ponieważ będzie on potrzebny w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="4df24-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="4df24-157">Dodawanie alertu tooyour zestawu skali maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4df24-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="4df24-158">Poniżej przedstawiono sposób która zawiera skrypt programu PowerShell tooadd alertu tooa zestawu skali maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4df24-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="4df24-159">Można znaleźć toohello po tooget hello nazwa alertu hello metryki toofire hello: [metryki wspólnej Skalowanie automatyczne Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4df24-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="4df24-160">Jest zalecana tooconfigure okna rozsądnym czasie hello alertu w kolejności tooavoid wyzwalania, skalowanie w pionie, wraz ze wszystkimi skojarzonymi przerw w obsłudze, zbyt często.</span><span class="sxs-lookup"><span data-stu-id="4df24-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="4df24-161">Należy wziąć pod uwagę okna o co najmniej 20-30 minut lub dłużej.</span><span class="sxs-lookup"><span data-stu-id="4df24-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="4df24-162">Należy wziąć pod uwagę poziomy skalowania, jeśli potrzebujesz tooavoid przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="4df24-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="4df24-163">Aby uzyskać więcej informacji dotyczących sposobu toocreate alerty można znaleźć toohello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="4df24-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="4df24-164">Przykładów dla platformy Azure Monitor PowerShell szybki start</span><span class="sxs-lookup"><span data-stu-id="4df24-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="4df24-165">Przykładów dla platformy Azure CLI wieloplatformowych Monitor szybki start</span><span class="sxs-lookup"><span data-stu-id="4df24-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="4df24-166">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4df24-166">Summary</span></span>
<span data-ttu-id="4df24-167">W tym artykule pokazano proste przykłady skalowania pionowej.</span><span class="sxs-lookup"><span data-stu-id="4df24-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="4df24-168">Te bloki konstrukcyjne — konto automatyzacji, elementy runbook, elementów webhook, alerty — może się łączyć szeroki zakres zdarzeń dostosowany zbiór akcji.</span><span class="sxs-lookup"><span data-stu-id="4df24-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
