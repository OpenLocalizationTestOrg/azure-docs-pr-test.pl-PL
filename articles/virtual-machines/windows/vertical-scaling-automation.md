---
title: "Automatyzacja Azure umożliwia skalowanie w pionie maszyn wirtualnych systemu Windows | Dokumentacja firmy Microsoft"
description: "Pionowo skalowania maszyny wirtualnej systemu Windows w odpowiedzi na monitorowanie alertów w usłudze Automatyzacja Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ea5169c1a95f00e78ae3f5f177812466eb7a0deb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="ea36f-103">Skalowanie w pionie maszyn wirtualnych systemu Windows w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="ea36f-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="ea36f-104">Skalowanie w pionie to proces zwiększania lub zmniejszania zasobów w odpowiedzi na obciążenie pracą maszyny.</span><span class="sxs-lookup"><span data-stu-id="ea36f-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="ea36f-105">W systemie Azure można to zrobić przez zmianę rozmiaru maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea36f-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="ea36f-106">Może to pomóc w następujących scenariuszach</span><span class="sxs-lookup"><span data-stu-id="ea36f-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="ea36f-107">Jeśli maszyna wirtualna nie jest często używany, można zmienić rozmiar go do mniejszy rozmiar, aby zmniejszyć koszty miesięcznego</span><span class="sxs-lookup"><span data-stu-id="ea36f-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="ea36f-108">Jeśli maszyna wirtualna ma do czynienia obciążenia szczytowego, można zmieniać na większy rozmiar, aby zwiększyć jego pojemność</span><span class="sxs-lookup"><span data-stu-id="ea36f-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="ea36f-109">Konspekt instrukcje w tym celu jest jako poniżej</span><span class="sxs-lookup"><span data-stu-id="ea36f-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="ea36f-110">Instalator usługi Automatyzacja Azure na dostęp do maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ea36f-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="ea36f-111">Importowanie elementów runbook skali pionowej automatyzacji Azure w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ea36f-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="ea36f-112">Dodawanie elementu webhook z elementem runbook</span><span class="sxs-lookup"><span data-stu-id="ea36f-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="ea36f-113">Dodawanie alertu do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ea36f-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="ea36f-114">Ze względu na rozmiar maszyny wirtualnej pierwszej rozmiary, do których może być skalowana, może być ograniczony z powodu dostępności bieżącej maszyny wirtualnej wdrożonej w innej wielkości w klastrze.</span><span class="sxs-lookup"><span data-stu-id="ea36f-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="ea36f-115">W elementach runbook automatyzacji opublikowanych używane w tym artykule zajmie się tym przypadku firma Microsoft i skalować tylko w ramach poniżej pary rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea36f-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="ea36f-116">Oznacza to, czy Standard_D1v2 maszyny wirtualnej zostanie nie nagle Skalowanie z Standard_G5 lub skalowany w dół do Basic_A0.</span><span class="sxs-lookup"><span data-stu-id="ea36f-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="ea36f-117">Rozmiary maszyn wirtualnych, skalowanie pary</span><span class="sxs-lookup"><span data-stu-id="ea36f-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="ea36f-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="ea36f-118">Basic_A0</span></span> |<span data-ttu-id="ea36f-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="ea36f-119">Basic_A4</span></span> |
> | <span data-ttu-id="ea36f-120">Standardowa_A0</span><span class="sxs-lookup"><span data-stu-id="ea36f-120">Standard_A0</span></span> |<span data-ttu-id="ea36f-121">Standardowa_A4</span><span class="sxs-lookup"><span data-stu-id="ea36f-121">Standard_A4</span></span> |
> | <span data-ttu-id="ea36f-122">Standardowa_A5</span><span class="sxs-lookup"><span data-stu-id="ea36f-122">Standard_A5</span></span> |<span data-ttu-id="ea36f-123">Standardowa_A7</span><span class="sxs-lookup"><span data-stu-id="ea36f-123">Standard_A7</span></span> |
> | <span data-ttu-id="ea36f-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="ea36f-124">Standard_A8</span></span> |<span data-ttu-id="ea36f-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="ea36f-125">Standard_A9</span></span> |
> | <span data-ttu-id="ea36f-126">Standardowa_A10</span><span class="sxs-lookup"><span data-stu-id="ea36f-126">Standard_A10</span></span> |<span data-ttu-id="ea36f-127">Standardowa_A11</span><span class="sxs-lookup"><span data-stu-id="ea36f-127">Standard_A11</span></span> |
> | <span data-ttu-id="ea36f-128">Standardowa_D1</span><span class="sxs-lookup"><span data-stu-id="ea36f-128">Standard_D1</span></span> |<span data-ttu-id="ea36f-129">Standardowa_D4</span><span class="sxs-lookup"><span data-stu-id="ea36f-129">Standard_D4</span></span> |
> | <span data-ttu-id="ea36f-130">Standardowa_D11</span><span class="sxs-lookup"><span data-stu-id="ea36f-130">Standard_D11</span></span> |<span data-ttu-id="ea36f-131">Standardowa_D14</span><span class="sxs-lookup"><span data-stu-id="ea36f-131">Standard_D14</span></span> |
> | <span data-ttu-id="ea36f-132">Standardowa_DS1</span><span class="sxs-lookup"><span data-stu-id="ea36f-132">Standard_DS1</span></span> |<span data-ttu-id="ea36f-133">Standardowa_DS4</span><span class="sxs-lookup"><span data-stu-id="ea36f-133">Standard_DS4</span></span> |
> | <span data-ttu-id="ea36f-134">Standardowa_DS11</span><span class="sxs-lookup"><span data-stu-id="ea36f-134">Standard_DS11</span></span> |<span data-ttu-id="ea36f-135">Standardowa_DS14</span><span class="sxs-lookup"><span data-stu-id="ea36f-135">Standard_DS14</span></span> |
> | <span data-ttu-id="ea36f-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="ea36f-136">Standard_D1v2</span></span> |<span data-ttu-id="ea36f-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="ea36f-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="ea36f-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="ea36f-138">Standard_D11v2</span></span> |<span data-ttu-id="ea36f-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="ea36f-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="ea36f-140">Standardowa_G1</span><span class="sxs-lookup"><span data-stu-id="ea36f-140">Standard_G1</span></span> |<span data-ttu-id="ea36f-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="ea36f-141">Standard_G5</span></span> |
> | <span data-ttu-id="ea36f-142">Standardowa_GS1</span><span class="sxs-lookup"><span data-stu-id="ea36f-142">Standard_GS1</span></span> |<span data-ttu-id="ea36f-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="ea36f-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="ea36f-144">Instalator usługi Automatyzacja Azure na dostęp do maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ea36f-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="ea36f-145">W pierwszej kolejności należy wykonać to utworzyć konto usługi Automatyzacja Azure, który będzie obsługiwał elementów runbook, używana do skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea36f-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale a Virtual Machine.</span></span> <span data-ttu-id="ea36f-146">Ostatnio usługi Automatyzacja wprowadzono funkcję "Konto Uruchom jako", co sprawia, że ustawienia zapasowej główną usługi dla automatycznie uruchomione elementy runbook w imieniu użytkownika bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="ea36f-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="ea36f-147">Możesz przeczytać więcej na temat tego artykułu poniżej:</span><span class="sxs-lookup"><span data-stu-id="ea36f-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="ea36f-148">Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ea36f-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="ea36f-149">Importowanie elementów runbook skali pionowej automatyzacji Azure w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ea36f-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="ea36f-150">Elementy runbook, które są potrzebne w pionie skalowania maszyny wirtualnej zostały już opublikowane w galerii elementu Runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="ea36f-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="ea36f-151">Konieczne będzie zaimportowanie ich do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ea36f-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="ea36f-152">Można poznać sposoby zaimportować elementy runbook, odczytując w następującym artykule.</span><span class="sxs-lookup"><span data-stu-id="ea36f-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="ea36f-153">Galeria elementów Runbook i modułów dla usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="ea36f-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="ea36f-154">Elementy runbook, które wymagają zaimportowania przedstawiono na poniższej ilustracji</span><span class="sxs-lookup"><span data-stu-id="ea36f-154">The runbooks that need to be imported are shown in the image below</span></span>

![Importowanie elementów runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="ea36f-156">Dodawanie elementu webhook z elementem runbook</span><span class="sxs-lookup"><span data-stu-id="ea36f-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="ea36f-157">Po zaimportowaniu elementów runbook, które będą potrzebne, aby dodać elementu webhook do elementu runbook, mogą być wyzwalane przez alert z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea36f-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="ea36f-158">Szczegółowe informacje o utworzeniu elementu webhook dla elementu Runbook, które mogą być odczytywane w tym miejscu</span><span class="sxs-lookup"><span data-stu-id="ea36f-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="ea36f-159">Azure automatyzacji elementów webhook</span><span class="sxs-lookup"><span data-stu-id="ea36f-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="ea36f-160">Upewnij się, że można skopiować elementu webhook przed zamknięciem okna dialogowego elementu webhook, ponieważ będzie on potrzebny w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ea36f-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="ea36f-161">Dodawanie alertu do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ea36f-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="ea36f-162">Wybierz ustawienia maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ea36f-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="ea36f-163">Wybierz opcję "Reguły alertu"</span><span class="sxs-lookup"><span data-stu-id="ea36f-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="ea36f-164">Wybierz opcję "Dodaj alert"</span><span class="sxs-lookup"><span data-stu-id="ea36f-164">Select "Add alert"</span></span>
4. <span data-ttu-id="ea36f-165">Wybierz metrykę, aby wyzwalać alert na</span><span class="sxs-lookup"><span data-stu-id="ea36f-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="ea36f-166">Wybierz warunek, w przypadku których spełnione będą powodować wyzwalać alert</span><span class="sxs-lookup"><span data-stu-id="ea36f-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="ea36f-167">Wybierz próg dla warunku w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="ea36f-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="ea36f-168">do spełnienia</span><span class="sxs-lookup"><span data-stu-id="ea36f-168">to be fulfilled</span></span>
7. <span data-ttu-id="ea36f-169">Wybierz okres służącym usługi monitorowania będzie sprawdzać, warunek i wartość progową kroki 5 i 6</span><span class="sxs-lookup"><span data-stu-id="ea36f-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="ea36f-170">Wklej skopiowane z poprzedniej sekcji elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="ea36f-170">Paste in the webhook you copied from the previous section.</span></span>

![Dodawanie alertu do maszyny wirtualnej 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Dodawanie alertu do maszyny wirtualnej 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

