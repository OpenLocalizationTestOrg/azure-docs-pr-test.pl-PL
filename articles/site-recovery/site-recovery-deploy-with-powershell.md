---
title: "aaaReplicate tooAzure maszyn wirtualnych funkcji Hyper-V w portalu klasycznym hello przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Automatyzowanie replikacji hello maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM przy użyciu usługi Site Recovery i programu PowerShell w portalu klasycznym hello"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="dbbfe-103">Replikowanie maszyn wirtualnych funkcji Hyper-V tooAzure przy użyciu programu PowerShell w portalu klasycznym hello</span><span class="sxs-lookup"><span data-stu-id="dbbfe-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dbbfe-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dbbfe-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="dbbfe-105">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dbbfe-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="dbbfe-106">Klasyczny portal</span><span class="sxs-lookup"><span data-stu-id="dbbfe-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="dbbfe-107">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="dbbfe-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="dbbfe-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="dbbfe-108">Overview</span></span>
<span data-ttu-id="dbbfe-109">Usługa Azure Site Recovery przyczynia się tooyour ciągłości i odzyskiwaniem po awarii (BCDR) odzyskiwania strategii biznesowej poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych w różnych scenariuszy wdrażania.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="dbbfe-110">Pełną listę wdrażania scenariuszy dla hello [Omówienie usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="dbbfe-111">W tym artykule opisano, jak toouse PowerShell tooautomate typowych zadań należy tooperform podczas konfigurowania maszyny wirtualne funkcji Hyper-V tooreplicate usługi Azure Site Recovery w magazynie tooAzure chmur programu System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="dbbfe-112">Hello artykuł zawiera wymagania wstępne dotyczące hello scenariusza i przedstawia sposób instalacji tooset się w magazynie usługi Site Recovery hello dostawcy usługi Azure Site Recovery na źródłowym serwerze programu VMM hello, Zarejestruj serwer hello w magazynie hello, Dodaj konto magazynu platformy Azure, zainstaluj hello Azure Agent usług odzyskiwania na serwerach hostów funkcji Hyper-V, skonfigurować ustawienia ochrony dla chmur programu VMM, które będzie zastosowane tooall chronionych maszyn wirtualnych, a następnie włącz ochronę tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="dbbfe-113">Aby zakończyć, testowania hello trybu failover toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="dbbfe-114">Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="dbbfe-115">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dbbfe-116">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="dbbfe-117">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="dbbfe-117">Before you start</span></span>
<span data-ttu-id="dbbfe-118">Upewnij się, że te wymagania wstępne zostały spełnione:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="dbbfe-119">Wymagania wstępne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dbbfe-119">Azure prerequisites</span></span>
* <span data-ttu-id="dbbfe-120">Będziesz potrzebować konta platformy [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="dbbfe-121">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="dbbfe-122">Będziesz potrzebować toostore replikowane dane konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="dbbfe-123">Konto Hello musi włączyć replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="dbbfe-124">Należy go w tym samym regionie co magazyn usługi Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="dbbfe-125">[Dowiedz się więcej na temat usługi Azure storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="dbbfe-126">Należy się upewnić, że maszyny wirtualne mają tooprotect są zgodne z toomake [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="dbbfe-127">Wymagania wstępne programu VMM</span><span class="sxs-lookup"><span data-stu-id="dbbfe-127">VMM prerequisites</span></span>
* <span data-ttu-id="dbbfe-128">Należy na serwerze programu VMM działa na System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="dbbfe-129">Będziesz potrzebować co najmniej jedna chmura na powitania serwera VMM ma tooprotect.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="dbbfe-130">Chmura Hello powinna zawierać:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="dbbfe-131">Co najmniej jedną grupę hostów programu VMM.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="dbbfe-132">Serwery hosta funkcji Hyper-V lub klastry w każdej grupie hostów.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="dbbfe-133">Co najmniej jednej maszyny wirtualnej na powitania serwera źródłowego funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="dbbfe-134">Wymagania wstępne funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="dbbfe-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="dbbfe-135">Witaj Serwery hosta funkcji Hyper-V musi działać co najmniej **systemu Windows Server 2012** z rolą funkcji Hyper-V lub **Microsoft Hyper-V Server 2012** i mieć hello zainstalowane najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="dbbfe-136">Jeśli używasz funkcji Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie, jeśli masz klaster oparty na statycznym adresie IP.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="dbbfe-137">Będziesz potrzebować brokera klastra hello tooconfigure ręcznie.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="dbbfe-138">toodo to w Menedżerze serwera > Menedżera klastra trybu Failover, kliknij pozycję Połącz klaster toohello **Konfiguruj rolę** i wybierz **brokera funkcji Hyper-V Replica** w hello **wybierz rolę**ekranie powitania Kreatora wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="dbbfe-139">Dowolnego serwera hosta funkcji Hyper-V lub klaster, dla którego ma zostać toomanage ochrony musi być uwzględniona w chmurze VMM.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="dbbfe-140">Wymagania wstępne związane z mapowaniem sieci</span><span class="sxs-lookup"><span data-stu-id="dbbfe-140">Network mapping prerequisites</span></span>
<span data-ttu-id="dbbfe-141">Podczas ochrony maszyn wirtualnych w sieci Azure mapowania mapuje między sieciami maszyn wirtualnych na źródłowym serwerze programu VMM hello a docelowej sieci platformy Azure tooenable hello następujące:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="dbbfe-142">Wszystkie komputery, które w tryb failover na powitania sam połączyć tooeach innych, niezależnie od tego, jakiego planu odzyskiwania, które znajdują się w sieci.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="dbbfe-143">Jeśli brama sieci została skonfigurowana w hello docelową sieć platformy Azure, maszyny wirtualne można łączyć z tooother lokalnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="dbbfe-144">Jeśli nie skonfigurujesz sieci mapowania tylko maszyny wirtualne, które awaryjnie w hello sam plan odzyskiwania będą mogli tooconnect tooeach innych po tooAzure pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="dbbfe-145">Jeśli chcesz, aby mapowanie sieci toodeploy potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="dbbfe-146">maszyny wirtualne Hello ma tooprotect na źródłowym serwerze programu VMM hello powinna być tooa połączonych sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="dbbfe-147">Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="dbbfe-148">Maszyny wirtualne replikowane toowhich sieć platformy Azure mogą łączyć po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="dbbfe-149">Należy wybrać tej sieci w czasie hello pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="dbbfe-150">Witaj sieć powinna znajdować się w hello tym samym regionie co subskrypcja usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="dbbfe-151">Wymagania wstępne programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbbfe-151">PowerShell prerequisites</span></span>
<span data-ttu-id="dbbfe-152">Upewnij się, że masz toogo gotowy programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="dbbfe-153">Jeśli korzystasz już z programu PowerShell, potrzebujesz tooupgrade tooversion 0.8.10 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="dbbfe-154">Aby uzyskać informacje o konfigurowaniu programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="dbbfe-155">Po należy skonfigurować i skonfigurowaniu programu PowerShell można wyświetlić wszystkie dostępne polecenia cmdlet hello hello usługi [tutaj](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="dbbfe-156">toolearn o porad ułatwiających przy użyciu poleceń cmdlet hello, takich jak jak wartości parametru, dane wejściowe i dane wyjściowe są zazwyczaj obsługiwane w programie Azure PowerShell, zobacz [wprowadzenie do poleceń cmdlet Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="dbbfe-157">Krok 1: Ustaw hello subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dbbfe-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="dbbfe-158">W programie PowerShell Uruchom te polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="dbbfe-159">Zastąp hello elementów w obrębie hello "< >" konkretnych informacji.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="dbbfe-160">Krok 2: Tworzenie magazynu usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="dbbfe-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="dbbfe-161">W programie PowerShell Zamień hello elementów w obrębie hello "< >" konkretnych informacji i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="dbbfe-162">Krok 3: Generowanie klucza rejestracji magazynu</span><span class="sxs-lookup"><span data-stu-id="dbbfe-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="dbbfe-163">Wygeneruj klucz rejestracji w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="dbbfe-164">Po pobraniu hello dostawcy usługi Azure Site Recovery i zainstaluj go na serwerze VMM hello, użyjesz tego serwera VMM hello tooregister kluczy w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="dbbfe-165">Pobierz plik ustawienia magazynu hello i Ustaw kontekst hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="dbbfe-166">Ustaw kontekst magazynu hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="dbbfe-167">Krok 4: Instalowanie hello dostawcy usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="dbbfe-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="dbbfe-168">Na maszynie VMM hello należy utworzyć katalog, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="dbbfe-169">Wyodrębnij pliki hello przy użyciu dostawcy hello pobrane, uruchamiając następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="dbbfe-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="dbbfe-170">Zainstaluj dostawcę hello przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-170">Install hello provider using hello following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="dbbfe-171">Poczekaj na powitania toofinish instalacji.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="dbbfe-172">Zarejestruj serwer hello w magazynie hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="dbbfe-173">Krok 5: Tworzenie konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dbbfe-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="dbbfe-174">Jeśli nie masz konta magazynu platformy Azure, Utwórz konto z włączoną replikacją geograficzną, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="dbbfe-175">Należy pamiętać, że konto magazynu hello musi być w tym samym regionie co usługa Azure Site Recovery hello hello i skojarzone z hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="dbbfe-176">Krok 6: Hello instalacji agenta usług odzyskiwania Azure</span><span class="sxs-lookup"><span data-stu-id="dbbfe-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="dbbfe-177">Z hello portalu Azure, zainstaluj agenta usług odzyskiwania Azure hello na każdym serwerze hosta funkcji Hyper-V znajdujących się w chmurach VMM hello mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="dbbfe-178">Uruchom następujące polecenie na wszystkich hostach VMM hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="dbbfe-179">Krok 7: Konfigurowanie chmury ustawienia ochrony</span><span class="sxs-lookup"><span data-stu-id="dbbfe-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="dbbfe-180">Utwórz tooAzure profilu ochrony chmury, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="dbbfe-181">Pobierz kontenera ochrony, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="dbbfe-182">Uruchom skojarzenie hello hello kontenera ochrony z chmurą hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="dbbfe-183">Po zakończeniu zadania hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="dbbfe-184">Po zakończeniu przetwarzania zadania hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-184">After hello job has finished processing, run hello following command:</span></span>

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



<span data-ttu-id="dbbfe-185">toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="dbbfe-186">Krok 8: Konfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="dbbfe-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="dbbfe-187">Przed rozpoczęciem mapowania sieci Sprawdź, czy maszyny wirtualne na źródłowym serwerze programu VMM hello są połączone tooa sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="dbbfe-188">Ponadto należy utworzyć jeden lub więcej sieci wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="dbbfe-189">Należy zauważyć, że wiele sieci maszyn wirtualnych mogą być mapowane tooa pojedynczej sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="dbbfe-190">Należy pamiętać, że jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="dbbfe-191">Jeśli nie istnieje docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="dbbfe-192">Witaj pierwsze polecenie pobiera serwerów hello bieżący magazyn Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="dbbfe-193">polecenie Hello przechowuje hello serwerów Microsoft Azure Site Recovery w hello $Servers tablicy zmiennej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="dbbfe-194">Hello drugie polecenie pobiera hello sieci odzyskiwania lokacji dla pierwszego serwera hello hello $Servers tablicy.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="dbbfe-195">polecenie Hello przechowuje hello sieci w zmiennej hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="dbbfe-196">trzecie polecenie Hello pobiera subskrypcji platformy Azure za pomocą polecenia cmdlet Get-AzureSubscription hello, a następnie zapisanie tej wartości w zmiennej hello $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="dbbfe-197">polecenie czwarty Hello pobiera sieci wirtualnych platformy Azure przy użyciu polecenia cmdlet Get-AzureVNetSite hello, a następnie tę wartość w zmiennej hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="dbbfe-198">polecenie cmdlet końcowego Hello tworzy mapowanie między hello sieci podstawowej i hello sieci maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="dbbfe-199">polecenia cmdlet Hello określa hello sieci podstawowej jako pierwszy element $Networks hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="dbbfe-200">polecenia cmdlet Hello określa sieć maszyny wirtualnej jako pierwszy element $AzureVmNetworks hello za pomocą jego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="dbbfe-201">polecenie Hello zawiera swój identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="dbbfe-202">Krok 9: Włączanie ochrony dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="dbbfe-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="dbbfe-203">Po serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="dbbfe-204">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-204">Note hello following:</span></span>

<span data-ttu-id="dbbfe-205">Maszyny wirtualne muszą spełniać [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="dbbfe-206">dla maszyny wirtualnej hello musi być ustawiona systemu operacyjnego hello ochrony tooenable i właściwości dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="dbbfe-207">Podczas tworzenia maszyny wirtualnej w programie VMM przy użyciu szablonu maszyny wirtualnej można ustawić właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="dbbfe-208">Można również ustawić te właściwości dla istniejących maszyn wirtualnych na powitania **ogólne** i **konfiguracja sprzętu** karty hello właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="dbbfe-209">Jeśli nie ustawisz tych właściwości w programie VMM będziesz w stanie tooconfigure je w portalu usługi Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="dbbfe-210">Ochrona tooenable hello uruchom następujące polecenia kontenera ochrony hello tooget:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="dbbfe-211">$ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="dbbfe-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="dbbfe-212">Pobierz jednostki ochrony hello (VM), uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="dbbfe-213">Włącz hello DR dla maszyny Wirtualnej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="dbbfe-214">Testowanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="dbbfe-214">Test your deployment</span></span>
<span data-ttu-id="dbbfe-215">Planowanie wdrożenia możesz uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania składające się z wielu maszyn wirtualnych i uruchomić test trybu failover dla hello tootest.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="dbbfe-216">Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="dbbfe-217">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-217">Note that:</span></span>

* <span data-ttu-id="dbbfe-218">Maszyna wirtualna toohello tooconnect na platformie Azure przy użyciu pulpitu zdalnego po hello w tryb failover, należy włączyć Podłączanie pulpitu zdalnego na maszynie wirtualnej hello przed rozpoczęciem powitalne testowy tryb failover.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="dbbfe-219">Po przejściu w tryb failover użyjesz publicznego adresu IP address tooconnect toohello maszynę wirtualną na platformie Azure przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="dbbfe-220">Jeśli chcesz toodo to, upewnij się, że nie ma żadnych zasad domeny, które uniemożliwiają łączącego tooa maszyny wirtualnej przy użyciu adresu publicznego.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="dbbfe-221">toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="dbbfe-222">Tworzenie planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="dbbfe-222">Create a recovery plan</span></span>
1. <span data-ttu-id="dbbfe-223">Utwórz plik .xml jako szablon dla planu odzyskiwania przy użyciu danych hello poniżej, a następnie zapisz go jako "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="dbbfe-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="dbbfe-224">Zmień węzeł RecoveryPlan hello identyfikator, nazwę PrimaryServerId i SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="dbbfe-225">Zmień węzeł ProtectionEntity hello PrimaryProtectionEntityId (vmid z programu VMM).</span><span class="sxs-lookup"><span data-stu-id="dbbfe-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="dbbfe-226">Możesz dodać więcej maszyn wirtualnych, dodając więcej węzłów ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="dbbfe-227">Wypełnij hello danych w szablonie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="dbbfe-228">Utwórz hello RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="dbbfe-229">Wykonywanie próby przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="dbbfe-229">Run a test failover</span></span>
1. <span data-ttu-id="dbbfe-230">Pobierz obiekt RecoveryPlan hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="dbbfe-231">$RPObject = get-AzureSiteRecoveryRecoveryPlan-Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="dbbfe-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="dbbfe-232">Uruchom hello testowy tryb failover, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dbbfe-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="dbbfe-233"><a name=monitor></a>Monitorowanie aktywności</span><span class="sxs-lookup"><span data-stu-id="dbbfe-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="dbbfe-234">Witaj Użyj następującego polecenia toomonitor hello działania.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="dbbfe-235">Należy pamiętać, że masz toowait Between zadania hello toofinish przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="dbbfe-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dbbfe-236">Next steps</span></span>
<span data-ttu-id="dbbfe-237">[Dowiedz się więcej](/powershell/azure/overview) o poleceniach cmdlet programu PowerShell systemu Azure lokacji odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="dbbfe-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="dbbfe-238"></a>.</span></span>
