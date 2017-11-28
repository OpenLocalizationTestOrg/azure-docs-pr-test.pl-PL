---
title: "Zarządzanie węzły obliczeniowe klastra HPC Pack | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat narzędzia skryptu programu PowerShell do dodawania, usuwania, uruchomić i zatrzymać węzły obliczeniowe klastra HPC Pack 2012 R2 na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="382ea-103">Zarządzanie liczbą i dostępnością węzłów obliczeniowych w klastrze pakietu HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="382ea-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="382ea-104">Jeśli utworzony klaster HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure, możesz sposobów, aby łatwo dodać, usunąć, start (zainicjować obsługi administracyjnej) lub zatrzymać (deprovision) obliczeniowe niektórych maszyn wirtualnych węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="382ea-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="382ea-105">Aby wykonać te zadania, uruchomić skrypty programu Azure PowerShell, które są zainstalowane w węźle głównym maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="382ea-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="382ea-106">Skrypty te można kontrolować liczbę i dostępności zasobów klastra HPC Pack, więc można kontrolować koszty.</span><span class="sxs-lookup"><span data-stu-id="382ea-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="382ea-107">Ten artykuł dotyczy tylko w klastrach HPC Pack 2012 R2 na platformie Azure utworzonych przy użyciu klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="382ea-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="382ea-108">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="382ea-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="382ea-109">Ponadto skrypty programu PowerShell opisanych w tym artykule nie są dostępne w HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="382ea-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="382ea-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="382ea-110">Prerequisites</span></span>
* <span data-ttu-id="382ea-111">**Klaster HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure**: Tworzenie klastra HPC Pack 2012 R2 w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="382ea-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="382ea-112">Na przykład można zautomatyzować wdrożenie przy użyciu obrazu HPC Pack 2012 R2 z maszyny Wirtualnej w portalu Azure Marketplace i skrypt programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="382ea-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="382ea-113">Aby uzyskać informacje i wymagania wstępne, zobacz [utworzyć klaster HPC z skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="382ea-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="382ea-114">Po wdrożeniu odnaleźć węzła zarządzania skryptów w folderze % CCP\_folder bin % głównej w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="382ea-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="382ea-115">Uruchamianie wszystkich skryptów jako administrator.</span><span class="sxs-lookup"><span data-stu-id="382ea-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="382ea-116">**Certyfikat zarządzania lub pliku ustawień publikowania na platformie Azure**: należy wykonać jedną z następujących czynności w węźle głównym:</span><span class="sxs-lookup"><span data-stu-id="382ea-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="382ea-117">**Plik ustawień publikowania importu platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="382ea-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="382ea-118">Aby to zrobić, uruchom następujące polecenia cmdlet programu Azure PowerShell w węźle głównym:</span><span class="sxs-lookup"><span data-stu-id="382ea-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="382ea-119">**Konfigurowanie certyfikatu zarządzania platformy Azure w węźle głównym**.</span><span class="sxs-lookup"><span data-stu-id="382ea-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="382ea-120">Jeśli plik cer, zaimportuj go w magazynie certyfikatów CurrentUser\My, a następnie uruchom następujące polecenie cmdlet programu Azure PowerShell do środowiska Azure (AzureCloud lub AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="382ea-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="382ea-121">Dodaj węzeł obliczeniowy maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="382ea-121">Add compute node VMs</span></span>
<span data-ttu-id="382ea-122">Dodaj węzły obliczeniowe z **HpcIaaSNode.ps1 Dodaj** skryptu.</span><span class="sxs-lookup"><span data-stu-id="382ea-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="382ea-123">Składnia</span><span class="sxs-lookup"><span data-stu-id="382ea-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="382ea-124">Parametry</span><span class="sxs-lookup"><span data-stu-id="382ea-124">Parameters</span></span>
* <span data-ttu-id="382ea-125">**ServiceName**: Nazwa usługi w chmurze, która obliczeniowe nowego węzła maszyny wirtualne są dodawane do.</span><span class="sxs-lookup"><span data-stu-id="382ea-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="382ea-126">**Nazwa_obrazu**: Nazwa obrazu maszyny Wirtualnej platformy Azure, który można uzyskać za pośrednictwem klasycznego portalu Azure lub polecenia cmdlet programu Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="382ea-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="382ea-127">Obraz musi spełniać następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="382ea-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="382ea-128">Musi być zainstalowany w systemie operacyjnym Windows.</span><span class="sxs-lookup"><span data-stu-id="382ea-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="382ea-129">HPC Pack musi być zainstalowany w roli węzła obliczeń.</span><span class="sxs-lookup"><span data-stu-id="382ea-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="382ea-130">Obraz musi być prywatny obrazu w kategorii użytkownika nie publicznego obrazu maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="382ea-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="382ea-131">**Ilość**: numer węzła obliczeniowego maszyn wirtualnych ma zostać dodana.</span><span class="sxs-lookup"><span data-stu-id="382ea-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="382ea-132">**InstanceSize**: rozmiar węzła obliczeniowego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="382ea-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="382ea-133">**DomainUserName**: nazwa użytkownika domeny, który jest używany do dołączania nowych maszyn wirtualnych do domeny.</span><span class="sxs-lookup"><span data-stu-id="382ea-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="382ea-134">**DomainUserPassword**: hasło użytkownika domeny.</span><span class="sxs-lookup"><span data-stu-id="382ea-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="382ea-135">**NodeNameSeries** (opcjonalnie): nazewnictwa wzorca dla węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="382ea-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="382ea-136">Musi mieć format &lt; *głównego\_nazwa*&gt;&lt;*Start\_numer*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="382ea-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="382ea-137">Na przykład MyCN % 10% oznacza serii od MyCN11 nazwy węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="382ea-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="382ea-138">Jeśli nie zostanie określony, skrypt używa skonfigurowanego węzeł nazwy serii w klastrze HPC.</span><span class="sxs-lookup"><span data-stu-id="382ea-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="382ea-139">Przykład</span><span class="sxs-lookup"><span data-stu-id="382ea-139">Example</span></span>
<span data-ttu-id="382ea-140">W poniższym przykładzie dodano 20 węzła obliczeń duży rozmiar maszyn wirtualnych w usłudze w chmurze *hpcservice1*, oparte na obrazie maszyny Wirtualnej *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="382ea-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="382ea-141">Usuń węzeł obliczeniowy maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="382ea-141">Remove compute node VMs</span></span>
<span data-ttu-id="382ea-142">Usuń węzły obliczeniowe z **HpcIaaSNode.ps1 Usuń** skryptu.</span><span class="sxs-lookup"><span data-stu-id="382ea-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="382ea-143">Składnia</span><span class="sxs-lookup"><span data-stu-id="382ea-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="382ea-144">Parametry</span><span class="sxs-lookup"><span data-stu-id="382ea-144">Parameters</span></span>
* <span data-ttu-id="382ea-145">**Nazwa**: nazwy węzłów klastra ma zostać usunięty.</span><span class="sxs-lookup"><span data-stu-id="382ea-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="382ea-146">Symbole wieloznaczne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="382ea-146">Wildcards are supported.</span></span> <span data-ttu-id="382ea-147">Nazwa zestawu parametru jest nazwa.</span><span class="sxs-lookup"><span data-stu-id="382ea-147">The parameter set name is Name.</span></span> <span data-ttu-id="382ea-148">Nie można określić zarówno **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="382ea-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="382ea-149">**Węzeł**: obiekt HpcNode dla węzłów do usunięcia, które można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="382ea-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="382ea-150">Nazwa zestawu parametrów jest węzeł.</span><span class="sxs-lookup"><span data-stu-id="382ea-150">The parameter set name is Node.</span></span> <span data-ttu-id="382ea-151">Nie można określić zarówno **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="382ea-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="382ea-152">**DeleteVHD** (opcjonalnie): ustawienie, aby usunąć skojarzone dyski dla maszyn wirtualnych, które zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="382ea-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="382ea-153">**Wymuś** (opcjonalnie): ustawienie, aby wymusić węzłów HPC w trybie offline przed ich usunięciem.</span><span class="sxs-lookup"><span data-stu-id="382ea-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="382ea-154">**Potwierdź** (opcjonalnie): monitu o potwierdzenie przed wykonaniem polecenia.</span><span class="sxs-lookup"><span data-stu-id="382ea-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="382ea-155">**WhatIf**: ustawienie, aby opisano, co się stanie, jeśli polecenie zostanie wykonane bez rzeczywistego wykonania polecenia.</span><span class="sxs-lookup"><span data-stu-id="382ea-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="382ea-156">Przykład</span><span class="sxs-lookup"><span data-stu-id="382ea-156">Example</span></span>
<span data-ttu-id="382ea-157">Poniższy przykład wymusza w trybie offline węzłach o nazwach od *HPCNode-CN -* i usuwa je węzły i ich skojarzone dyski.</span><span class="sxs-lookup"><span data-stu-id="382ea-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="382ea-158">Węzeł obliczeń początkowy maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="382ea-158">Start compute node VMs</span></span>
<span data-ttu-id="382ea-159">Start obliczeniowe węzłów o **Start HpcIaaSNode.ps1** skryptu.</span><span class="sxs-lookup"><span data-stu-id="382ea-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="382ea-160">Składnia</span><span class="sxs-lookup"><span data-stu-id="382ea-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="382ea-161">Parametry</span><span class="sxs-lookup"><span data-stu-id="382ea-161">Parameters</span></span>
* <span data-ttu-id="382ea-162">**Nazwa**: nazwy węzłów klastra ma zostać uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="382ea-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="382ea-163">Symbole wieloznaczne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="382ea-163">Wildcards are supported.</span></span> <span data-ttu-id="382ea-164">Nazwa zestawu parametru jest nazwa.</span><span class="sxs-lookup"><span data-stu-id="382ea-164">The parameter set name is Name.</span></span> <span data-ttu-id="382ea-165">Nie można określić zarówno **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="382ea-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="382ea-166">**Węzeł**-HpcNode obiektu dla węzłów, które ma zostać uruchomiony, które można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="382ea-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="382ea-167">Nazwa zestawu parametrów jest węzeł.</span><span class="sxs-lookup"><span data-stu-id="382ea-167">The parameter set name is Node.</span></span> <span data-ttu-id="382ea-168">Nie można określić zarówno **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="382ea-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="382ea-169">Przykład</span><span class="sxs-lookup"><span data-stu-id="382ea-169">Example</span></span>
<span data-ttu-id="382ea-170">Węzły w poniższym przykładzie rozpoczyna się od nazwy rozpoczynające się *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="382ea-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="382ea-171">Zatrzymaj węźle obliczeń maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="382ea-171">Stop compute node VMs</span></span>
<span data-ttu-id="382ea-172">Zatrzymaj węzły obliczeniowe z **Stop HpcIaaSNode.ps1** skryptu.</span><span class="sxs-lookup"><span data-stu-id="382ea-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="382ea-173">Składnia</span><span class="sxs-lookup"><span data-stu-id="382ea-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="382ea-174">Parametry</span><span class="sxs-lookup"><span data-stu-id="382ea-174">Parameters</span></span>
* <span data-ttu-id="382ea-175">**Nazwa**-nazwy węzłów klastra, aby zostać zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="382ea-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="382ea-176">Symbole wieloznaczne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="382ea-176">Wildcards are supported.</span></span> <span data-ttu-id="382ea-177">Nazwa zestawu parametru jest nazwa.</span><span class="sxs-lookup"><span data-stu-id="382ea-177">The parameter set name is Name.</span></span> <span data-ttu-id="382ea-178">Nie można określić zarówno **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="382ea-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="382ea-179">**Węzeł**: obiekt HpcNode dla węzłów, które ma zostać zatrzymany, których można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="382ea-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="382ea-180">Nazwa zestawu parametrów jest węzeł.</span><span class="sxs-lookup"><span data-stu-id="382ea-180">The parameter set name is Node.</span></span> <span data-ttu-id="382ea-181">Nie można określić zarówno **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="382ea-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="382ea-182">**Wymuś** (opcjonalnie): ustawienie, aby wymusić węzłów HPC w trybie offline przed zatrzymaniem je.</span><span class="sxs-lookup"><span data-stu-id="382ea-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="382ea-183">Przykład</span><span class="sxs-lookup"><span data-stu-id="382ea-183">Example</span></span>
<span data-ttu-id="382ea-184">Poniższy przykład wymusza węzłów w trybie offline z nazwami od *HPCNode-CN -* , a następnie zatrzymuje węzłów.</span><span class="sxs-lookup"><span data-stu-id="382ea-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="382ea-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="382ea-185">Next steps</span></span>
* <span data-ttu-id="382ea-186">Aby automatycznie zwiększać i zmniejszać węzłów klastra, zgodnie z bieżące obciążenie zadań i zadań w klastrze, zobacz [automatycznie zwiększyć lub zmniejszyć zasobów klastra HPC Pack na platformie Azure zgodnie z obciążenie klastra](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="382ea-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

