---
title: "węzły obliczeniowe klastra HPC Pack aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o tooadd narzędzia skrypt programu PowerShell, Usuń, start i Zatrzymaj węzły obliczeniowe klastra HPC Pack 2012 R2 na platformie Azure"
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
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="f502c-103">Zarządzanie numer hello i dostępności węzłów obliczeniowych w klastrze HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f502c-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="f502c-104">Utworzono klaster HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure, możesz się, że sposoby tooeasily Dodawanie, usuwanie, start (zainicjować obsługi administracyjnej) lub niektóre Zatrzymaj (deprovision) obliczeniowe maszyn wirtualnych węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="f502c-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="f502c-105">toodo te zadania są uruchamiane skrypty programu Azure PowerShell, które są zainstalowane w węźle głównym hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f502c-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="f502c-106">Skrypty te umożliwiają kontrolę liczby hello i dostępności zasobów klastra HPC Pack, można kontrolować koszty.</span><span class="sxs-lookup"><span data-stu-id="f502c-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f502c-107">Ten artykuł dotyczy tylko tooHPC Pack 2012 R2 klastrów w systemie Azure utworzonych przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f502c-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="f502c-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f502c-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="f502c-109">Ponadto hello skryptów programu PowerShell opisanych w tym artykule nie są dostępne w HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="f502c-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f502c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f502c-110">Prerequisites</span></span>
* <span data-ttu-id="f502c-111">**Klaster HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure**: Tworzenie klastra HPC Pack 2012 R2 w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f502c-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="f502c-112">Na przykład można zautomatyzować hello wdrożenia przy użyciu obrazu HPC Pack 2012 R2 wirtualna hello w portalu Azure Marketplace hello i skrypt programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="f502c-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="f502c-113">Aby uzyskać informacje i wymagania wstępne, zobacz [utworzyć klaster HPC z hello skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="f502c-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="f502c-114">Po wdrożeniu Znajdź hello skrypty zarządzania węzła w lokalizacji % hello CCP\_folder bin % głównej na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="f502c-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="f502c-115">Uruchomić skrypty hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f502c-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="f502c-116">**Certyfikat zarządzania lub pliku ustawień publikowania na platformie Azure**: należy toodo jedną z następujących hello na powitania węzła głównego:</span><span class="sxs-lookup"><span data-stu-id="f502c-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="f502c-117">**Plik ustawień publikowania importu hello Azure**.</span><span class="sxs-lookup"><span data-stu-id="f502c-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="f502c-118">toodo tego hello uruchom następujące polecenia cmdlet programu PowerShell Azure na powitania węzła głównego:</span><span class="sxs-lookup"><span data-stu-id="f502c-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="f502c-119">**Konfigurowanie certyfikatu zarządzania platformy Azure hello na powitania węzła głównego**.</span><span class="sxs-lookup"><span data-stu-id="f502c-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="f502c-120">Jeśli plik .cer hello, zaimportuj go w magazynie certyfikatów CurrentUser\My hello, a następnie uruchom następujące polecenia cmdlet programu PowerShell Azure do środowiska Azure (AzureCloud lub AzureChinaCloud) hello:</span><span class="sxs-lookup"><span data-stu-id="f502c-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="f502c-121">Dodaj węzeł obliczeniowy maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="f502c-121">Add compute node VMs</span></span>
<span data-ttu-id="f502c-122">Dodaj węzły obliczeniowe z hello **HpcIaaSNode.ps1 Dodaj** skryptu.</span><span class="sxs-lookup"><span data-stu-id="f502c-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="f502c-123">Składnia</span><span class="sxs-lookup"><span data-stu-id="f502c-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="f502c-124">Parametry</span><span class="sxs-lookup"><span data-stu-id="f502c-124">Parameters</span></span>
* <span data-ttu-id="f502c-125">**ServiceName**: Nazwa hello usługi w chmurze obliczeniowe nowego węzła maszyny wirtualne są dodawane do.</span><span class="sxs-lookup"><span data-stu-id="f502c-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="f502c-126">**Nazwa_obrazu**: Nazwa obrazu maszyny Wirtualnej platformy Azure, który można uzyskać za pośrednictwem hello klasycznego portalu Azure lub polecenia cmdlet programu Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="f502c-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="f502c-127">Obraz powitania musi spełniać następujące wymagania hello:</span><span class="sxs-lookup"><span data-stu-id="f502c-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="f502c-128">Musi być zainstalowany w systemie operacyjnym Windows.</span><span class="sxs-lookup"><span data-stu-id="f502c-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="f502c-129">HPC Pack musi być zainstalowany w roli węzła obliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="f502c-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="f502c-130">Obraz powitania musi być prywatny obrazu w kategorii użytkownika hello nie publicznego obrazu maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f502c-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="f502c-131">**Ilość**: liczba toobe maszyn wirtualnych węzła obliczeń dodane.</span><span class="sxs-lookup"><span data-stu-id="f502c-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="f502c-132">**InstanceSize**: rozmiar hello obliczeniowe węzła maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f502c-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="f502c-133">**DomainUserName**: nazwa użytkownika domeny, które jest używane toojoin hello nowej domeny toohello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f502c-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="f502c-134">**DomainUserPassword**: hasło użytkownika domeny hello.</span><span class="sxs-lookup"><span data-stu-id="f502c-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="f502c-135">**NodeNameSeries** (opcjonalnie): wzorzec nazewnictwa dla hello węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="f502c-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="f502c-136">musi mieć Hello format &lt; *głównego\_nazwa*&gt;&lt;*Start\_numer*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="f502c-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="f502c-137">Na przykład MyCN % 10% środki szeregów hello obliczeniowe od MyCN11 nazwy węzła.</span><span class="sxs-lookup"><span data-stu-id="f502c-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="f502c-138">Jeśli nie zostanie określony, hello skrypt używa hello skonfigurowany nazwy serii węzła w klastrze HPC hello.</span><span class="sxs-lookup"><span data-stu-id="f502c-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="f502c-139">Przykład</span><span class="sxs-lookup"><span data-stu-id="f502c-139">Example</span></span>
<span data-ttu-id="f502c-140">Witaj poniższy przykład umożliwia dodanie 20 węzła obliczeń duży rozmiar maszyn wirtualnych w usłudze w chmurze hello *hpcservice1*, oparte na obrazie maszyny Wirtualnej hello *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="f502c-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="f502c-141">Usuń węzeł obliczeniowy maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="f502c-141">Remove compute node VMs</span></span>
<span data-ttu-id="f502c-142">Usuń węzły obliczeniowe z hello **HpcIaaSNode.ps1 Usuń** skryptu.</span><span class="sxs-lookup"><span data-stu-id="f502c-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="f502c-143">Składnia</span><span class="sxs-lookup"><span data-stu-id="f502c-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="f502c-144">Parametry</span><span class="sxs-lookup"><span data-stu-id="f502c-144">Parameters</span></span>
* <span data-ttu-id="f502c-145">**Nazwa**: usunięte nazwy toobe węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="f502c-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="f502c-146">Symbole wieloznaczne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f502c-146">Wildcards are supported.</span></span> <span data-ttu-id="f502c-147">Nazwa zestawu parametrów Hello jest.</span><span class="sxs-lookup"><span data-stu-id="f502c-147">hello parameter set name is Name.</span></span> <span data-ttu-id="f502c-148">Nie można określić zarówno hello **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="f502c-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="f502c-149">**Węzeł**: obiekt HpcNode powitania dla toobe węzłów hello usunięty, który można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC hello [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="f502c-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="f502c-150">Nazwa zestawu parametrów Hello jest węzeł.</span><span class="sxs-lookup"><span data-stu-id="f502c-150">hello parameter set name is Node.</span></span> <span data-ttu-id="f502c-151">Nie można określić zarówno hello **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="f502c-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="f502c-152">**DeleteVHD** (opcjonalnie): ustawienie toodelete hello skojarzone dyski hello maszyn wirtualnych, które zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="f502c-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="f502c-153">**Wymuś** (opcjonalnie): ustawienie tooforce węzłów HPC w trybie offline przed ich usunięciem.</span><span class="sxs-lookup"><span data-stu-id="f502c-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="f502c-154">**Potwierdź** (opcjonalnie): monitu o potwierdzenie przed wykonaniem polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="f502c-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="f502c-155">**WhatIf**: ustawienie toodescribe, co się stanie, jeśli wykonywane hello polecenie bez rzeczywistego wykonania polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="f502c-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="f502c-156">Przykład</span><span class="sxs-lookup"><span data-stu-id="f502c-156">Example</span></span>
<span data-ttu-id="f502c-157">Witaj poniższy przykład wymusza węzłów hello w trybie offline z nazwami od *HPCNode-CN -* i usuwa je hello węzły i ich skojarzone dyski.</span><span class="sxs-lookup"><span data-stu-id="f502c-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="f502c-158">Węzeł obliczeń początkowy maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="f502c-158">Start compute node VMs</span></span>
<span data-ttu-id="f502c-159">Start obliczeniowe węzłów o hello **Start HpcIaaSNode.ps1** skryptu.</span><span class="sxs-lookup"><span data-stu-id="f502c-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="f502c-160">Składnia</span><span class="sxs-lookup"><span data-stu-id="f502c-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="f502c-161">Parametry</span><span class="sxs-lookup"><span data-stu-id="f502c-161">Parameters</span></span>
* <span data-ttu-id="f502c-162">**Nazwa**: nazwy toobe węzłów klastra hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f502c-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="f502c-163">Symbole wieloznaczne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f502c-163">Wildcards are supported.</span></span> <span data-ttu-id="f502c-164">Nazwa zestawu parametrów Hello jest.</span><span class="sxs-lookup"><span data-stu-id="f502c-164">hello parameter set name is Name.</span></span> <span data-ttu-id="f502c-165">Nie można określić zarówno hello **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="f502c-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="f502c-166">**Węzeł**-obiekt HpcNode powitania dla toobe węzłów hello pracę, który można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC hello [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="f502c-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="f502c-167">Nazwa zestawu parametrów Hello jest węzeł.</span><span class="sxs-lookup"><span data-stu-id="f502c-167">hello parameter set name is Node.</span></span> <span data-ttu-id="f502c-168">Nie można określić zarówno hello **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="f502c-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="f502c-169">Przykład</span><span class="sxs-lookup"><span data-stu-id="f502c-169">Example</span></span>
<span data-ttu-id="f502c-170">Witaj poniższy przykład węzłów rozpoczyna się od nazwy rozpoczynające się *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="f502c-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="f502c-171">Zatrzymaj węźle obliczeń maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="f502c-171">Stop compute node VMs</span></span>
<span data-ttu-id="f502c-172">Zatrzymaj węzły obliczeniowe z hello **Stop HpcIaaSNode.ps1** skryptu.</span><span class="sxs-lookup"><span data-stu-id="f502c-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="f502c-173">Składnia</span><span class="sxs-lookup"><span data-stu-id="f502c-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="f502c-174">Parametry</span><span class="sxs-lookup"><span data-stu-id="f502c-174">Parameters</span></span>
* <span data-ttu-id="f502c-175">**Nazwa**-nazwy toobe węzłów klastra hello zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="f502c-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="f502c-176">Symbole wieloznaczne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f502c-176">Wildcards are supported.</span></span> <span data-ttu-id="f502c-177">Nazwa zestawu parametrów Hello jest.</span><span class="sxs-lookup"><span data-stu-id="f502c-177">hello parameter set name is Name.</span></span> <span data-ttu-id="f502c-178">Nie można określić zarówno hello **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="f502c-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="f502c-179">**Węzeł**: obiekt HpcNode powitania dla toobe węzłów hello zatrzymana, który można uzyskać za pomocą polecenia cmdlet środowiska PowerShell klastra HPC hello [błędzie Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="f502c-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="f502c-180">Nazwa zestawu parametrów Hello jest węzeł.</span><span class="sxs-lookup"><span data-stu-id="f502c-180">hello parameter set name is Node.</span></span> <span data-ttu-id="f502c-181">Nie można określić zarówno hello **nazwa** i **węzła** parametrów.</span><span class="sxs-lookup"><span data-stu-id="f502c-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="f502c-182">**Wymuś** (opcjonalnie): ustawienie tooforce węzłów HPC w trybie offline przed zatrzymaniem je.</span><span class="sxs-lookup"><span data-stu-id="f502c-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="f502c-183">Przykład</span><span class="sxs-lookup"><span data-stu-id="f502c-183">Example</span></span>
<span data-ttu-id="f502c-184">Witaj poniższy przykład wymusza węzłów w trybie offline z nazwami od *HPCNode-CN -* , a następnie zatrzymuje hello węzłów.</span><span class="sxs-lookup"><span data-stu-id="f502c-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="f502c-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f502c-185">Next steps</span></span>
* <span data-ttu-id="f502c-186">tooautomatically wzrostu albo zmniejszyć węzłów klastra hello zgodnie z hello bieżące obciążenie zadań i zadań w klastrze hello, zobacz [automatycznie zwiększyć lub zmniejszyć zasobów klastra HPC Pack hello Azure zgodnie z obciążenie klastra toohello](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="f502c-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

