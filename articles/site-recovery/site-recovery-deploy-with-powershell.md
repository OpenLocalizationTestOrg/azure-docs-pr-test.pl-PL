---
title: "Replikowanie maszyn wirtualnych funkcji Hyper-V do platformy Azure w klasycznym portalu przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Automatyzowanie replikacji maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM przy użyciu usługi Site Recovery i programu PowerShell w klasycznym portalu"
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
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="c7355-103">Replikowanie maszyn wirtualnych funkcji Hyper-V do platformy Azure przy użyciu programu PowerShell w klasycznym portalu</span><span class="sxs-lookup"><span data-stu-id="c7355-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7355-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c7355-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="c7355-105">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7355-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="c7355-106">Klasyczny portal</span><span class="sxs-lookup"><span data-stu-id="c7355-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="c7355-107">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="c7355-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="c7355-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c7355-108">Overview</span></span>
<span data-ttu-id="c7355-109">Usługa Azure Site Recovery przyczynia się do strategii biznesowej ciągłości i odzyskiwaniem po awarii odzyskiwania (BCDR) poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych w różnych scenariuszy wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c7355-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="c7355-110">Pełną listę wdrażania scenariuszy dla [Omówienie usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7355-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="c7355-111">W tym artykule przedstawiono sposób automatyzacji typowych zadań, które należy wykonać podczas konfigurowania usługi Azure Site Recovery do replikowania maszyn wirtualnych funkcji Hyper-V w chmurach programu System Center VMM do magazynu platformy Azure przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7355-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="c7355-112">Artykuł zawiera wymagania wstępne dla scenariusza i przedstawiono sposób konfigurowania magazynu usługi Site Recovery, zainstaluj dostawcę usługi Azure Site Recovery na źródłowym serwerze programu VMM, Zarejestruj serwer w magazynie, dodawania konta magazynu platformy Azure, zainstaluj agenta usług odzyskiwania Azure na serwerach hostów funkcji Hyper-V, skonfigurować ustawienia ochrony dla chmur programu VMM, które będą stosowane do wszystkich chronionych maszyn wirtualnych , a następnie włącz ochronę tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c7355-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="c7355-113">Aby zakończyć, przetestuj tryb failover w celu sprawdzenia, czy wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="c7355-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="c7355-114">Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c7355-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="c7355-115">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c7355-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c7355-116">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c7355-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="c7355-117">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c7355-117">Before you start</span></span>
<span data-ttu-id="c7355-118">Upewnij się, że te wymagania wstępne zostały spełnione:</span><span class="sxs-lookup"><span data-stu-id="c7355-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="c7355-119">Wymagania wstępne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c7355-119">Azure prerequisites</span></span>
* <span data-ttu-id="c7355-120">Będziesz potrzebować konta platformy [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="c7355-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="c7355-121">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7355-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c7355-122">Będziesz potrzebować konta magazynu Azure do przechowywania replikowanych danych.</span><span class="sxs-lookup"><span data-stu-id="c7355-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="c7355-123">Konto musi włączyć replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="c7355-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="c7355-124">Powinien znajdować się w tym samym regionie co magazyn usługi Azure Site Recovery i być skojarzone z tą samą subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="c7355-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="c7355-125">[Dowiedz się więcej na temat usługi Azure storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7355-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="c7355-126">Należy się upewnić, że maszyny wirtualne, które mają być chronione są zgodne z [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="c7355-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="c7355-127">Wymagania wstępne programu VMM</span><span class="sxs-lookup"><span data-stu-id="c7355-127">VMM prerequisites</span></span>
* <span data-ttu-id="c7355-128">Należy na serwerze programu VMM działa na System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="c7355-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="c7355-129">Będziesz potrzebować co najmniej jednej chmury na serwerze programu VMM, który chcesz chronić.</span><span class="sxs-lookup"><span data-stu-id="c7355-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="c7355-130">Chmura powinna zawierać:</span><span class="sxs-lookup"><span data-stu-id="c7355-130">The cloud should contain:</span></span>
  * <span data-ttu-id="c7355-131">Co najmniej jedną grupę hostów programu VMM.</span><span class="sxs-lookup"><span data-stu-id="c7355-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="c7355-132">Serwery hosta funkcji Hyper-V lub klastry w każdej grupie hostów.</span><span class="sxs-lookup"><span data-stu-id="c7355-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="c7355-133">Co najmniej jednej maszyny wirtualnej na serwerze źródłowym funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c7355-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="c7355-134">Wymagania wstępne funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="c7355-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="c7355-135">Serwery hosta funkcji Hyper-V musi działać co najmniej **systemu Windows Server 2012** z rolą funkcji Hyper-V lub **Microsoft Hyper-V Server 2012** i mieć zainstalowane najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="c7355-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="c7355-136">Jeśli używasz funkcji Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie, jeśli masz klaster oparty na statycznym adresie IP.</span><span class="sxs-lookup"><span data-stu-id="c7355-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="c7355-137">Konieczne będzie ręczne skonfigurowanie brokera klastra.</span><span class="sxs-lookup"><span data-stu-id="c7355-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="c7355-138">W tym celu w Menedżerze serwera > Menedżera klastra trybu Failover, kliknij pozycję Połącz się z klastrem **Konfiguruj rolę** i wybierz **brokera funkcji Hyper-V Replica** w **wybierz rolę** ekran Kreatora wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="c7355-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="c7355-139">Dowolnego serwera hosta funkcji Hyper-V lub klastra, dla którego chcesz zarządzać ochrony musi być uwzględniona w chmurze VMM.</span><span class="sxs-lookup"><span data-stu-id="c7355-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="c7355-140">Wymagania wstępne związane z mapowaniem sieci</span><span class="sxs-lookup"><span data-stu-id="c7355-140">Network mapping prerequisites</span></span>
<span data-ttu-id="c7355-141">Gdy chronisz maszyny wirtualne na platformie Azure, mapowanie sieci działa między źródłowymi sieciami maszyny wirtualnej na źródłowym serwerze programu VMM a docelowymi sieciami platformy Azure. Dzięki temu dostępne są następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c7355-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="c7355-142">Wszystkie komputery, które nie przejdą pomyślnie za pośrednictwem tej sieci można połączyć ze sobą, niezależnie od tego, jakiego planu odzyskiwania znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="c7355-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="c7355-143">Jeśli brama sieci została skonfigurowana w docelowej sieci platformy Azure, maszyny wirtualne mogą łączyć się z innymi lokalnymi maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="c7355-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="c7355-144">Jeśli nie skonfigurujesz mapowania sieci, tylko maszyny wirtualne, które przechodzą w tryb failover w tym samym planie odzyskiwania, będą mogły się ze sobą łączyć po przejściu w tryb failover na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7355-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="c7355-145">Jeśli chcesz wdrożyć mapowanie sieci, musisz upewnić się, że spełnione są następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="c7355-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="c7355-146">Maszyny wirtualne, które chcesz chronić na źródłowym serwerze programu VMM, powinny być połączone z siecią maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c7355-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="c7355-147">Ta sieć powinna być połączona z siecią logiczną skojarzoną z chmurą.</span><span class="sxs-lookup"><span data-stu-id="c7355-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="c7355-148">Sieć platformy Azure, z którą replikowane maszyny wirtualne mogą łączyć się po przejściu w tryb failover na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7355-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="c7355-149">Tę sieć wybierzesz podczas przejścia w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="c7355-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="c7355-150">Sieć powinna znajdować się w tym samym regionie co subskrypcja usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c7355-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="c7355-151">Wymagania wstępne programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7355-151">PowerShell prerequisites</span></span>
<span data-ttu-id="c7355-152">Upewnij się, że masz przejść programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7355-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="c7355-153">Jeśli korzystasz już z programu PowerShell, należy uaktualnić do wersji 0.8.10 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c7355-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="c7355-154">Aby uzyskać informacje o konfigurowaniu programu PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="c7355-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="c7355-155">Po należy skonfigurować i skonfigurowaniu programu PowerShell można wyświetlić wszystkie dostępne polecenia cmdlet dla usługi [tutaj](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c7355-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="c7355-156">Aby dowiedzieć się więcej o wskazówki, które mogą pomóc używać poleceń cmdlet, takich jak jak wartości parametru, dane wejściowe i dane wyjściowe są zazwyczaj obsługiwane w programie Azure PowerShell, zobacz [wprowadzenie do poleceń cmdlet Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="c7355-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="c7355-157">Krok 1: Ustaw subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c7355-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="c7355-158">W programie PowerShell Uruchom te polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7355-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="c7355-159">Zastąp elementy wewnątrz "< >" konkretnych informacji.</span><span class="sxs-lookup"><span data-stu-id="c7355-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="c7355-160">Krok 2: Tworzenie magazynu usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c7355-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="c7355-161">W programie PowerShell Zastąp elementy wewnątrz "< >" konkretnych informacji i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7355-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="c7355-162">Krok 3: Generowanie klucza rejestracji magazynu</span><span class="sxs-lookup"><span data-stu-id="c7355-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="c7355-163">Wygeneruj klucz rejestracji magazynu.</span><span class="sxs-lookup"><span data-stu-id="c7355-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="c7355-164">Po pobraniu dostawcy usługi Azure Site Recovery i zainstalowaniu go na serwerze programu VMM użyjesz tego klucza do zarejestrowania serwera programu VMM w magazynie.</span><span class="sxs-lookup"><span data-stu-id="c7355-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="c7355-165">Pobierz plik ustawienia magazynu i Ustaw kontekst:</span><span class="sxs-lookup"><span data-stu-id="c7355-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="c7355-166">Ustaw kontekst magazynu, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7355-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="c7355-167">Krok 4: Instalowanie dostawcy usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c7355-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="c7355-168">Na maszynie VMM należy utworzyć katalog, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="c7355-169">Wyodrębnij pliki przy użyciu pobranego dostawcy, uruchamiając następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="c7355-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="c7355-170">Zainstaluj dostawcę przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="c7355-170">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="c7355-171">Poczekaj na zakończenie instalacji.</span><span class="sxs-lookup"><span data-stu-id="c7355-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="c7355-172">Zarejestruj serwer w magazynie przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7355-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="c7355-173">Krok 5: Tworzenie konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c7355-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="c7355-174">Jeśli nie masz konta magazynu platformy Azure, Utwórz konto włączona replikacja geograficzna, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="c7355-175">Należy pamiętać, że konto magazynu musi znajdować się w tym samym regionie co usługa Azure Site Recovery i musi być skojarzony z tą samą subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="c7355-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="c7355-176">Krok 6: Zainstaluj agenta usług odzyskiwania Azure</span><span class="sxs-lookup"><span data-stu-id="c7355-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="c7355-177">W portalu Azure Zainstaluj agenta usług odzyskiwania Azure na każdym serwerze hosta funkcji Hyper-V znajdujących się w chmurach programu VMM, który chcesz chronić.</span><span class="sxs-lookup"><span data-stu-id="c7355-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="c7355-178">Uruchom następujące polecenie na wszystkich hostach VMM:</span><span class="sxs-lookup"><span data-stu-id="c7355-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="c7355-179">Krok 7: Konfigurowanie chmury ustawienia ochrony</span><span class="sxs-lookup"><span data-stu-id="c7355-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="c7355-180">Utwórz profil ochrony chmury Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="c7355-181">Pobierz kontenera ochrony, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="c7355-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="c7355-182">Uruchom skojarzenie kontenera ochrony z chmurą:</span><span class="sxs-lookup"><span data-stu-id="c7355-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="c7355-183">Po zakończeniu zadania, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="c7355-184">Po zakończeniu przetwarzania zadania, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-184">After the job has finished processing, run the following command:</span></span>

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



<span data-ttu-id="c7355-185">Aby sprawdzić zakończenie operacji, postępuj zgodnie z instrukcjami [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="c7355-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="c7355-186">Krok 8: Konfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="c7355-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="c7355-187">Przed rozpoczęciem mapowania sieci należy się upewnić, że maszyny wirtualne na źródłowym serwerze programu VMM są połączone z siecią maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7355-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="c7355-188">Ponadto należy utworzyć jeden lub więcej sieci wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7355-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="c7355-189">Wiele sieci maszyn wirtualnych można mapować do pojedynczej sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7355-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="c7355-190">Jeśli sieć docelowa ma wiele podsieci i jedna z tych podsieci ma taką samą nazwę jak podsieć, w której znajduje się źródłowa maszyna wirtualna, replika maszyny wirtualnej zostanie podłączona do tej docelowej podsieci po przejściu w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="c7355-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="c7355-191">Jeśli nie istnieje docelowa podsieć o pasującej nazwie, maszyny wirtualnej zostaną podłączone do pierwszej podsieci w sieci.</span><span class="sxs-lookup"><span data-stu-id="c7355-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="c7355-192">Pierwsze polecenie pobiera serwerów dla bieżącego magazynu Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c7355-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="c7355-193">Polecenie zapisuje serwerów Microsoft Azure Site Recovery w zmiennej tablicy $Servers.</span><span class="sxs-lookup"><span data-stu-id="c7355-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="c7355-194">Drugie polecenie pobiera sieci odzyskiwania lokacji dla pierwszego serwera w tablicy $Servers.</span><span class="sxs-lookup"><span data-stu-id="c7355-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="c7355-195">Polecenie zapisuje sieci w zmiennej $Networks.</span><span class="sxs-lookup"><span data-stu-id="c7355-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="c7355-196">Trzecie polecenie pobiera subskrypcji platformy Azure za pomocą polecenia cmdlet Get-AzureSubscription, a następnie zapisanie tej wartości w zmiennej $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c7355-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="c7355-197">Polecenie czwarty pobiera sieci wirtualnych platformy Azure przy użyciu polecenia cmdlet Get-AzureVNetSite, a następnie tę wartość w zmiennej $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="c7355-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="c7355-198">Końcowe polecenie cmdlet tworzy mapowanie między sieci podstawowej i sieci maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7355-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="c7355-199">Polecenie cmdlet określa sieci podstawowej jako pierwszy element $Networks.</span><span class="sxs-lookup"><span data-stu-id="c7355-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="c7355-200">Polecenie cmdlet określa sieć maszyny wirtualnej jako pierwszy element $AzureVmNetworks za pomocą jego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c7355-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="c7355-201">Polecenie zawiera swój identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7355-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="c7355-202">Krok 9: Włączanie ochrony dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c7355-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="c7355-203">Po poprawnym skonfigurowaniu serwerów, chmur i sieci można włączyć ochronę dla maszyn wirtualnych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c7355-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="c7355-204">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="c7355-204">Note the following:</span></span>

<span data-ttu-id="c7355-205">Maszyny wirtualne muszą spełniać [wymagania wstępne maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="c7355-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="c7355-206">Aby włączyć ochronę, należy ustawić właściwości systemu operacyjnego i dysku systemu operacyjnego dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7355-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="c7355-207">Podczas tworzenia maszyny wirtualnej w programie VMM przy użyciu szablonu maszyny wirtualnej można ustawić właściwości.</span><span class="sxs-lookup"><span data-stu-id="c7355-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="c7355-208">Można również ustawić te właściwości dla istniejących maszyn wirtualnych na kartach **Ogólne** i **Konfiguracja sprzętu** właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7355-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="c7355-209">Jeśli nie ustawisz tych właściwości w programie VMM, możesz skonfigurować je w portalu Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c7355-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="c7355-210">Aby włączyć ochronę, uruchom następujące polecenie, aby pobrać kontenera ochrony:</span><span class="sxs-lookup"><span data-stu-id="c7355-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="c7355-211">$ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="c7355-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="c7355-212">Pobierz jednostki ochrony (VM), uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="c7355-213">Włącz DR dla maszyny Wirtualnej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="c7355-214">Testowanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c7355-214">Test your deployment</span></span>
<span data-ttu-id="c7355-215">Aby przetestować wdrożenie można uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania uwzględniający wiele maszyn wirtualnych i testować tryb failover planu.</span><span class="sxs-lookup"><span data-stu-id="c7355-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="c7355-216">Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej.</span><span class="sxs-lookup"><span data-stu-id="c7355-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="c7355-217">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="c7355-217">Note that:</span></span>

* <span data-ttu-id="c7355-218">Jeśli chcesz nawiązać połączenie z maszyną wirtualną na platformie Azure przy użyciu Pulpitu zdalnego po przejściu w tryb failover, włącz funkcję Podłączanie pulpitu zdalnego na maszynie wirtualnej przed rozpoczęciem próby przejścia w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="c7355-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="c7355-219">Po przejściu w tryb failover użyjesz publicznego adresu IP nawiązywania połączenia z maszyną wirtualną na platformie Azure przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="c7355-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="c7355-220">Jeśli chcesz to zrobić, upewnij się, że nie ma żadnych zasad domeny, które uniemożliwiają połączenie z maszyną wirtualną przy użyciu adresu publicznego.</span><span class="sxs-lookup"><span data-stu-id="c7355-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="c7355-221">Aby sprawdzić zakończenie operacji, postępuj zgodnie z instrukcjami [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="c7355-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="c7355-222">Tworzenie planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="c7355-222">Create a recovery plan</span></span>
1. <span data-ttu-id="c7355-223">Utwórz plik .xml jako szablon dla planu odzyskiwania przy użyciu danych poniżej, a następnie zapisz go jako "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="c7355-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="c7355-224">Zmień węzeł RecoveryPlan identyfikator, nazwę, PrimaryServerId i SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="c7355-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="c7355-225">Zmień węzeł ProtectionEntity PrimaryProtectionEntityId (vmid z programu VMM).</span><span class="sxs-lookup"><span data-stu-id="c7355-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="c7355-226">Możesz dodać więcej maszyn wirtualnych, dodając więcej węzłów ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="c7355-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="c7355-227">Wypełnij danych w szablonie:</span><span class="sxs-lookup"><span data-stu-id="c7355-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="c7355-228">Utwórz RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="c7355-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="c7355-229">Wykonywanie próby przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="c7355-229">Run a test failover</span></span>
1. <span data-ttu-id="c7355-230">Pobierz obiekt RecoveryPlan, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="c7355-231">$RPObject = get-AzureSiteRecoveryRecoveryPlan-Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="c7355-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="c7355-232">Uruchom test trybu failover, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7355-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="c7355-233"><a name=monitor></a>Monitorowanie aktywności</span><span class="sxs-lookup"><span data-stu-id="c7355-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="c7355-234">Użyj następujących poleceń, aby monitorować aktywność.</span><span class="sxs-lookup"><span data-stu-id="c7355-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="c7355-235">Należy pamiętać, że należy poczekać Between zadania do przetwarzania zakończyć.</span><span class="sxs-lookup"><span data-stu-id="c7355-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="c7355-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7355-236">Next steps</span></span>
<span data-ttu-id="c7355-237">[Dowiedz się więcej](/powershell/azure/overview) o poleceniach cmdlet programu PowerShell systemu Azure lokacji odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c7355-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="c7355-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="c7355-238"></a>.</span></span>
