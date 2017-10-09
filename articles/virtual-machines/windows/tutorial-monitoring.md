---
title: aaaAzure monitorowanie i maszyn wirtualnych z systemem Windows | Dokumentacja firmy Microsoft
description: "Samouczek — Monitor maszyny wirtualnej systemu Windows przy użyciu programu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="ac2f2-103">Umożliwia monitorowanie maszyny wirtualnej systemu Windows przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac2f2-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="ac2f2-104">Azure monitorowanie używa rozruchu toocollect agentów i danych dotyczących wydajności z maszyn wirtualnych platformy Azure, przechowywania tych danych w magazynie Azure i był dostępny za pośrednictwem portalu, hello modułu Azure PowerShell i hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="ac2f2-105">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ac2f2-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ac2f2-106">Włącz diagnostykę rozruchu na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="ac2f2-107">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="ac2f2-107">View boot diagnostics</span></span>
> * <span data-ttu-id="ac2f2-108">Wyświetlaj metryki hosta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-108">View VM host metrics</span></span>
> * <span data-ttu-id="ac2f2-109">Zainstaluj rozszerzenie diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="ac2f2-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="ac2f2-110">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-110">View VM metrics</span></span>
> * <span data-ttu-id="ac2f2-111">Utwórz alert</span><span class="sxs-lookup"><span data-stu-id="ac2f2-111">Create an alert</span></span>
> * <span data-ttu-id="ac2f2-112">Skonfiguruj zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="ac2f2-112">Set up advanced monitoring</span></span>

<span data-ttu-id="ac2f2-113">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ac2f2-114">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="ac2f2-115">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ac2f2-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="ac2f2-116">przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="ac2f2-117">Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="ac2f2-118">Podczas pracy samouczkiem hello, zastąp nazwę maszyny Wirtualnej, lokalizacji i grupy zasobów hello w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="ac2f2-119">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="ac2f2-119">View boot diagnostics</span></span>

<span data-ttu-id="ac2f2-120">Jak rozruchu maszyn wirtualnych systemu Windows, agenta diagnostyki rozruchu hello przechwytuje danych wyjściowych ekranu, który może służyć do rozwiązywania problemów z celem.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="ac2f2-121">Ta funkcja jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-121">This capability is enabled by default.</span></span> <span data-ttu-id="ac2f2-122">Hello przechwycony ekran zrzuty są przechowywane na koncie magazynu platformy Azure, tworzona jest również domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="ac2f2-123">Można uzyskać danych diagnostycznych hello rozruchu z hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="ac2f2-124">W hello poniższy przykład, diagnostyki rozruchu są toohello pobranego katalogu głównego hello * c:\* dysku.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="ac2f2-125">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="ac2f2-125">View host metrics</span></span>

<span data-ttu-id="ac2f2-126">Maszyny Wirtualnej systemu Windows ma dedykowanego hosta maszyny Wirtualnej na platformie Azure, która współdziała ona z.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="ac2f2-127">Metryki są automatycznie pobierane dla hello hosta i mogą być wyświetlane w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="ac2f2-128">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ac2f2-129">Kliknij przycisk **metryki** na hello bloku maszyny Wirtualnej, a następnie wybierz dowolną hello hosta metryki w obszarze **dostępne metryki** toosee jak wykonuje hello hosta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Wyświetlaj metryki hosta](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="ac2f2-131">Zainstaluj rozszerzenie diagnostyki</span><span class="sxs-lookup"><span data-stu-id="ac2f2-131">Install diagnostics extension</span></span>

<span data-ttu-id="ac2f2-132">Witaj hosta podstawowe metryki są dostępne, ale toosee bardziej szczegółowe i metryki specyficzne dla maszyny Wirtualnej, możesz tooneed tooinstall hello Azure diagnostics rozszerzenia na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="ac2f2-133">Witaj rozszerzenia diagnostyki Azure umożliwia dodatkowe funkcje monitorowania i diagnostyki toobe dane pobrane z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="ac2f2-134">Możesz wyświetlić te metryki wydajności i tworzyć alerty oparte na sposób wykonywania hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="ac2f2-135">rozszerzenie diagnostycznych Hello jest instalowany za pośrednictwem portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ac2f2-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="ac2f2-136">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ac2f2-137">Kliknij przycisk **ustawienia diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="ac2f2-138">Lista Hello wskazuje, że *diagnostyki rozruchu* są już włączone w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="ac2f2-139">Kliknij pole wyboru hello *podstawowe metryki*.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="ac2f2-140">Kliknij przycisk hello **Włącz monitorowanie na poziomie gościa** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Wyświetlaj metryki diagnostycznych](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="ac2f2-142">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-142">View VM metrics</span></span>

<span data-ttu-id="ac2f2-143">Witaj metryki maszyny Wirtualnej można wyświetlić w hello taki sam sposób, aby wyświetlić metryki maszyny Wirtualnej hosta hello:</span><span class="sxs-lookup"><span data-stu-id="ac2f2-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="ac2f2-144">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ac2f2-145">toosee wykonuje hello maszyny Wirtualnej, kliknij **metryki** na hello bloku maszyny Wirtualnej, a następnie wybierz dowolną hello diagnostyki metryki w obszarze **dostępne metryki**.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Wyświetlaj metryki maszyny Wirtualnej](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="ac2f2-147">Tworzenie alertów</span><span class="sxs-lookup"><span data-stu-id="ac2f2-147">Create alerts</span></span>

<span data-ttu-id="ac2f2-148">Można tworzyć alertów w oparciu metryki dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="ac2f2-149">Alerty można używane toonotify, który podczas średniego użycia procesora CPU przekracza określonego progu lub wolnego miejsca na dysku spada poniżej pewnego, np.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="ac2f2-150">Alerty są wyświetlane w portalu Azure hello lub mogą być wysyłane za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="ac2f2-151">W odpowiedzi tooalerts generowaną może także wyzwolić elementu runbook usługi Automatyzacja Azure lub usługi Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="ac2f2-152">Witaj poniższy przykład tworzy alert dla średniego użycia procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="ac2f2-153">W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ac2f2-154">Kliknij przycisk **reguły alertów** na powitania bloku maszyny Wirtualnej, następnie kliknij przycisk **Dodaj alert metryki** hello górze hello blok alerty.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="ac2f2-155">Podaj **nazwa** alertu, takie jak *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="ac2f2-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="ac2f2-156">tootrigger alert, gdy procent użycia procesora CPU przekracza 1.0 przez pięć minut, pozostaw hello wszystkich innych wartości domyślnych wybrane.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="ac2f2-157">Opcjonalnie, zaznacz pole hello *E-mail właściciele, współautorzy i czytelnicy* toosend powiadomienia e-mail.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="ac2f2-158">Akcja domyślna Hello jest toopresent powiadomienia w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="ac2f2-159">Kliknij przycisk hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="ac2f2-160">Zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="ac2f2-160">Advanced monitoring</span></span> 

<span data-ttu-id="ac2f2-161">Możliwość bardziej zaawansowane monitorowanie maszyny wirtualnej za pomocą [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="ac2f2-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="ac2f2-162">Jeśli nie zostało to jeszcze zrobione, należy zarejestrować się w celu [bezpłatnej wersji próbnej](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) programu Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="ac2f2-163">Jeśli masz portalu OMS toohello dostępu można znaleźć identyfikator obszaru roboczego hello klucza i obszar roboczy w bloku ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="ac2f2-164">Użyj hello [AzureRmVMExtension zestaw](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) przekazana tootooadd hello OMS rozszerzenia toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="ac2f2-165">Aktualizacja hello zmiennej wartości w hello poniżej przykładowy tooreflect możesz OMS klucz obszaru roboczego i identyfikator obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="ac2f2-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="ac2f2-166">Po upływie kilku minut powinien zostać wyświetlony hello nowej maszyny Wirtualnej w obszarze roboczym pakietu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![Blok OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="ac2f2-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac2f2-168">Next steps</span></span>
<span data-ttu-id="ac2f2-169">W tym samouczku został skonfigurowany i przejrzeć maszyn wirtualnych w Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="ac2f2-170">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="ac2f2-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ac2f2-171">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-171">Create a virtual network</span></span>
> * <span data-ttu-id="ac2f2-172">Tworzenie grupy zasobów i maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="ac2f2-173">Włącz diagnostykę rozruchu na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="ac2f2-174">Wyświetlanie diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="ac2f2-174">View boot diagnostics</span></span>
> * <span data-ttu-id="ac2f2-175">Wyświetlaj metryki hosta</span><span class="sxs-lookup"><span data-stu-id="ac2f2-175">View host metrics</span></span>
> * <span data-ttu-id="ac2f2-176">Zainstaluj rozszerzenie diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="ac2f2-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="ac2f2-177">Wyświetlaj metryki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ac2f2-177">View VM metrics</span></span>
> * <span data-ttu-id="ac2f2-178">Utwórz alert</span><span class="sxs-lookup"><span data-stu-id="ac2f2-178">Create an alert</span></span>
> * <span data-ttu-id="ac2f2-179">Skonfiguruj zaawansowane monitorowanie</span><span class="sxs-lookup"><span data-stu-id="ac2f2-179">Set up advanced monitoring</span></span>

<span data-ttu-id="ac2f2-180">Przejdź dalej toolearn samouczka toohello temat Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="ac2f2-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac2f2-181">Zarządzanie zabezpieczeniami maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ac2f2-181">Manage VM security</span></span>](./tutorial-azure-security.md)