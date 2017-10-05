---
title: "Replikowanie maszyn wirtualnych funkcji Hyper-V w programie VMM do lokacji dodatkowej przy użyciu programu PowerShell (usługi Azure Resource Manager) | Dokumentacja firmy Microsoft"
description: "Opisuje sposób wdrażania usługi Azure Site Recovery do organizowania replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V w chmurach VMM do dodatkowej lokacji programu VMM przy użyciu programu PowerShell (Resource Manager)"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="b3969-103">Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach VMM do dodatkowej lokacji programu VMM przy użyciu programu PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="b3969-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3969-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b3969-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="b3969-105">Klasyczny portal</span><span class="sxs-lookup"><span data-stu-id="b3969-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="b3969-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3969-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="b3969-107">Azure Site Recovery — Zapraszamy!</span><span class="sxs-lookup"><span data-stu-id="b3969-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="b3969-108">Użycie tego artykułu, jeśli chcesz replikować maszyny wirtualne funkcji Hyper-V lokalnego zarządzane w chmurach programu System Center Virtual Machine Manager (VMM) do lokacji dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="b3969-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="b3969-109">W tym artykule przedstawiono sposób automatyzacji typowych zadań, które należy wykonać podczas konfigurowania usługi Azure Site Recovery do replikowania maszyn wirtualnych funkcji Hyper-V w chmurach programu System Center VMM do programu System Center VMM chmur w lokacji dodatkowej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3969-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="b3969-110">Artykuł zawiera wymagania wstępne dla scenariusza i przedstawiono</span><span class="sxs-lookup"><span data-stu-id="b3969-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="b3969-111">Jak skonfigurować magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b3969-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="b3969-112">Zainstaluj dostawcę usługi Azure Site Recovery na serwerze VMM źródłowym i docelowym serwerze VMM</span><span class="sxs-lookup"><span data-stu-id="b3969-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="b3969-113">Zarejestrować serwery programu VMM w magazynie</span><span class="sxs-lookup"><span data-stu-id="b3969-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="b3969-114">Skonfiguruj zasady replikacji dla chmury VMM.</span><span class="sxs-lookup"><span data-stu-id="b3969-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="b3969-115">Ustawienia replikacji w zasadach zostaną zastosowane do wszystkich chronionych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="b3969-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="b3969-116">Włącz ochronę maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3969-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="b3969-117">Testowanie pracy awaryjnej maszyn wirtualnych, pojedynczo lub w ramach planu odzyskiwania, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="b3969-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="b3969-118">Wykonaj planowane lub nieplanowane przełączenie awaryjne maszyn wirtualnych, pojedynczo lub w ramach planu odzyskiwania, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="b3969-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="b3969-119">Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b3969-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="b3969-120">Platforma Azure ma dwa różne [modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md) związane z tworzeniem zasobów i pracą z nimi: Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="b3969-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="b3969-121">Platforma Azure ma dwa portale — klasyczny portal Azure, który obsługuje klasyczny model wdrażania, oraz portal Azure, który obsługuje oba modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="b3969-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="b3969-122">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3969-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="b3969-123">Lokalne wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3969-123">On-premises prerequisites</span></span>
<span data-ttu-id="b3969-124">Oto, co musisz w lokacjach głównych i dodatkowych lokalnymi wdrożyć ten scenariusz:</span><span class="sxs-lookup"><span data-stu-id="b3969-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="b3969-125">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="b3969-125">**Prerequisites**</span></span> | <span data-ttu-id="b3969-126">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="b3969-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="b3969-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="b3969-127">**VMM**</span></span> |<span data-ttu-id="b3969-128">Zaleca się wdrożenie serwer VMM w lokacji głównej, a serwer programu VMM w lokacji dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="b3969-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="b3969-129">Możesz również [replikacji między chmurami na jednym serwerze VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="b3969-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="b3969-130">W tym celu należy co najmniej dwóch chmur skonfigurowane na serwerze programu VMM.</span><span class="sxs-lookup"><span data-stu-id="b3969-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="b3969-131">Serwery VMM powinna być uruchomiona co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami.</span><span class="sxs-lookup"><span data-stu-id="b3969-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="b3969-132">Każdy serwer VMM musi mieć jedną lub więcej chmur skonfigurowane i wszystkich chmur musi mieć zestawu profilu pojemności funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3969-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="b3969-133">Chmury muszą zawierać co najmniej jedną grupę hostów programu VMM.</span><span class="sxs-lookup"><span data-stu-id="b3969-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="b3969-134">Dowiedz się więcej o konfigurowaniu chmur VMM w [Konfigurowanie przez Menedżera maszyny Wirtualnej w chmurze sieci szkieletowej](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), i [wskazówki: tworzenie chmur prywatnych z programu System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3969-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="b3969-135">Program VMM serwery powinny mieć dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="b3969-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="b3969-136">**Funkcja Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="b3969-136">**Hyper-V**</span></span> |<span data-ttu-id="b3969-137">Serwery funkcji Hyper-V musi działać co najmniej Windows Server 2012 z rolą funkcji Hyper-V i mieć zainstalowane najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="b3969-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="b3969-138">Serwer funkcji Hyper-V powinien zawierać co najmniej jedną maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b3969-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="b3969-139">Serwery hosta funkcji Hyper-V powinien znajdować się w grupach hostów w głównych i dodatkowych chmurach VMM.</span><span class="sxs-lookup"><span data-stu-id="b3969-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="b3969-140">Jeśli używasz funkcji Hyper-V w klastrze systemu Windows Server 2012 R2 należy zainstalować [zaktualizować 2961977](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="b3969-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="b3969-141">Jeśli korzystasz z funkcji Hyper-V w klastrze na Uwaga systemu Windows Server 2012 broker klastra nie jest tworzony automatycznie w przypadku statycznej klastra oparte na adresie IP.</span><span class="sxs-lookup"><span data-stu-id="b3969-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="b3969-142">Konieczne będzie ręczne skonfigurowanie brokera klastra.</span><span class="sxs-lookup"><span data-stu-id="b3969-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="b3969-143">[Dowiedz się więcej](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3969-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="b3969-144">**Dostawca**</span><span class="sxs-lookup"><span data-stu-id="b3969-144">**Provider**</span></span> |<span data-ttu-id="b3969-145">Podczas wdrażania usługi Site Recovery należy zainstalować dostawcę usługi Azure Site Recovery na serwerach VMM.</span><span class="sxs-lookup"><span data-stu-id="b3969-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="b3969-146">Dostawca komunikuje się z usługą Site Recovery za pośrednictwem protokołu HTTPS 443 do organizowania replikacji.</span><span class="sxs-lookup"><span data-stu-id="b3969-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="b3969-147">Dane replikacji między podstawowe i pomocnicze serwery funkcji Hyper-V za pośrednictwem sieci LAN lub połączenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="b3969-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="b3969-148">Dostawca uruchomiony na serwerze VMM musi mieć dostęp do tych adresów URL: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="b3969-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="b3969-149">Ponadto Zezwalaj na komunikację zapory z serwerów programu VMM do [zakresy IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) i Zezwalaj na protokół HTTPS (port 443).</span><span class="sxs-lookup"><span data-stu-id="b3969-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="b3969-150">Wymagania wstępne związane z mapowaniem sieci</span><span class="sxs-lookup"><span data-stu-id="b3969-150">Network mapping prerequisites</span></span>
<span data-ttu-id="b3969-151">Mapowanie sieci działa między sieciami maszyn wirtualnych VMM na serwerach VMM podstawowych i pomocniczych, aby:</span><span class="sxs-lookup"><span data-stu-id="b3969-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="b3969-152">Optymalnie umieścić po pracy awaryjnej maszyn wirtualnych repliki dodatkowej hosty funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3969-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="b3969-153">Połączenie maszyn wirtualnych repliki do odpowiedniej sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3969-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="b3969-154">Jeśli nie zostanie skonfigurowana sieć mapowania repliki maszyn wirtualnych nie będzie podłączona do żadnej sieci po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="b3969-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="b3969-155">Aby skonfigurować sieć mapowania podczas odzyskiwania lokacji w tym miejscu wdrożenia to co jest potrzebne:</span><span class="sxs-lookup"><span data-stu-id="b3969-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="b3969-156">Upewnij się, że maszyny wirtualne na źródłowym serwerze hosta funkcji Hyper-V są podłączone do sieci maszyny wirtualnej VMM.</span><span class="sxs-lookup"><span data-stu-id="b3969-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="b3969-157">Ta sieć powinna być połączona z siecią logiczną skojarzoną z chmurą.</span><span class="sxs-lookup"><span data-stu-id="b3969-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="b3969-158">Sprawdź, czy dodatkowej chmury, które będzie używane do odzyskiwania ma skonfigurowane odpowiednie sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3969-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="b3969-159">Ta sieć maszyn wirtualnych powinna być połączona z siecią logiczną skojarzoną z chmurą dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="b3969-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="b3969-160">Dowiedz się więcej na temat konfigurowania sieci w programie VMM w poniżej artykułów</span><span class="sxs-lookup"><span data-stu-id="b3969-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="b3969-161">Jak skonfigurować sieci logiczne w programie VMM</span><span class="sxs-lookup"><span data-stu-id="b3969-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="b3969-162">Konfigurowanie sieci Vmnetwork i bram w programie VMM</span><span class="sxs-lookup"><span data-stu-id="b3969-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="b3969-163">[Dowiedz się więcej](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) o tym, jak działa mapowanie sieci.</span><span class="sxs-lookup"><span data-stu-id="b3969-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="b3969-164">Wymagania wstępne programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3969-164">PowerShell prerequisites</span></span>
<span data-ttu-id="b3969-165">Upewnij się, że masz przejść programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3969-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="b3969-166">Jeśli korzystasz już z programu PowerShell, należy uaktualnić do wersji 0.8.10 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b3969-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="b3969-167">Aby uzyskać informacje o konfigurowaniu programu PowerShell, zobacz [Przewodnik instalowania i konfigurowania programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b3969-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="b3969-168">Po należy skonfigurować i skonfigurowaniu programu PowerShell można wyświetlić wszystkie dostępne polecenia cmdlet dla usługi [tutaj](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3969-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="b3969-169">Aby dowiedzieć się więcej o wskazówki, które mogą pomóc używać poleceń cmdlet, takich jak jak wartości parametru, dane wejściowe i dane wyjściowe są zazwyczaj obsługiwane w programie Azure PowerShell, zobacz [przewodnik Wprowadzenie do poleceń cmdlet Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="b3969-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="b3969-170">Krok 1: Ustaw subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b3969-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="b3969-171">Z programu Azure powershell, zaloguj się do konta platformy Azure: za pomocą następujących poleceń cmdlet</span><span class="sxs-lookup"><span data-stu-id="b3969-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="b3969-172">Pobierz listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b3969-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="b3969-173">Będzie to również listę subscriptionIDs dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b3969-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="b3969-174">Zanotuj identyfikator subskrypcji subskrypcji, w którym chcesz utworzyć magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b3969-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="b3969-175">Ustaw subskrypcji, w którym ma być tworzony, podając identyfikator subskrypcji magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b3969-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="b3969-176">Krok 2. Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b3969-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="b3969-177">Tworzenie grupy zasobów platformy Azure Resource Manager, jeśli nie masz już</span><span class="sxs-lookup"><span data-stu-id="b3969-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="b3969-178">Utwórz nowy magazyn usług odzyskiwania i zapisać utworzony obiekt magazynu ASR w zmiennej (zostanie później użyty).</span><span class="sxs-lookup"><span data-stu-id="b3969-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="b3969-179">Można również pobrać za pomocą polecenia cmdlet Get-AzureRMRecoveryServicesVault tworzenie post ASR magazynu obiektów:-</span><span class="sxs-lookup"><span data-stu-id="b3969-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="b3969-180">Krok 3: Ustaw kontekst magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b3969-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="b3969-181">Jeśli masz już utworzony magazyn, uruchom poniżej polecenie, aby uzyskać magazyn.</span><span class="sxs-lookup"><span data-stu-id="b3969-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="b3969-182">Ustaw kontekst magazynu, uruchamiając poniżej polecenia.</span><span class="sxs-lookup"><span data-stu-id="b3969-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="b3969-183">Krok 4: Instalowanie dostawcy usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b3969-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="b3969-184">Na maszynie VMM należy utworzyć katalog, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3969-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="b3969-185">Wyodrębnij pliki przy użyciu pobranego dostawcy, uruchamiając następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="b3969-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="b3969-186">Zainstaluj dostawcę przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="b3969-186">Install the provider using the following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="b3969-187">Poczekaj na zakończenie instalacji.</span><span class="sxs-lookup"><span data-stu-id="b3969-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="b3969-188">Zarejestruj serwer w magazynie przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b3969-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="b3969-189">Krok 5: Utwórz i Skojarz zasady replikacji</span><span class="sxs-lookup"><span data-stu-id="b3969-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="b3969-190">Utwórz zasady replikacji funkcji Hyper-V 2012 R2, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3969-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="b3969-191">Chmury VMM może zawierać hosty funkcji Hyper-V z różnymi wersjami systemu Windows Server (jak wspomniano w wymagania wstępne funkcji Hyper-V), ale zasady replikacji jest właściwego dla wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3969-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="b3969-192">Jeśli masz różnych hostach z systemem w wersji systemów operacyjnych, następnie utwórz zasady replikacji osobne dla każdego typu wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3969-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="b3969-193">Aby uzyskać np: Jeśli masz pięć hostów z uruchomionym systemem Windows 2012 serwerów i trzech w systemie Windows Server 2012 R2, należy utworzyć dwa zasady replikacji — po jednej dla każdego typu wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3969-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="b3969-194">Pobierz kontener ochronę podstawową (podstawowy chmury VMM) i odzyskiwania kontenera ochrony (odzyskiwania chmury VMM), uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="b3969-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="b3969-195">Pobrać zasady, który został utworzony w kroku 1 przy użyciu przyjaznej nazwy zasady</span><span class="sxs-lookup"><span data-stu-id="b3969-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="b3969-196">Uruchom skojarzenie kontenera ochrony (w chmurze VMM) z zasadami replikacji:</span><span class="sxs-lookup"><span data-stu-id="b3969-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="b3969-197">Poczekaj na ukończenie zadania skojarzenia zasad.</span><span class="sxs-lookup"><span data-stu-id="b3969-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="b3969-198">Można sprawdzić, czy ukończeniu zadania przy użyciu następującego fragmentu kodu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3969-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="b3969-199">Po zakończeniu przetwarzania zadania, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3969-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="b3969-200">Aby sprawdzić zakończenie operacji, postępuj zgodnie z instrukcjami [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="b3969-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="b3969-201">Krok 6: Skonfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="b3969-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="b3969-202">Pierwsze polecenie pobiera serwerów dla bieżącego magazynu Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b3969-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="b3969-203">Polecenie zapisuje serwerów Microsoft Azure Site Recovery w zmiennej tablicy $Servers.</span><span class="sxs-lookup"><span data-stu-id="b3969-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="b3969-204">Poniżej polecenia Pobierz sieci odzyskiwania lokacji na serwerze VMM źródłowym i docelowym serwerze VMM.</span><span class="sxs-lookup"><span data-stu-id="b3969-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="b3969-205">Źródłowy serwer VMM może być pierwszy lub drugi w tablicy serwerów.</span><span class="sxs-lookup"><span data-stu-id="b3969-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="b3969-206">Sprawdź nazwy serwerów programu VMM i odpowiednio uzyskać sieci</span><span class="sxs-lookup"><span data-stu-id="b3969-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="b3969-207">Końcowe polecenie cmdlet tworzy mapowanie między sieci podstawowej i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="b3969-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="b3969-208">Polecenie cmdlet określa sieci podstawowej jako pierwszy element $PrimaryNetworks i sieć odzyskiwania jako pierwszy element $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="b3969-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="b3969-209">Krok 7: Konfigurowanie mapowania magazynu</span><span class="sxs-lookup"><span data-stu-id="b3969-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="b3969-210">Poniżej polecenie pobiera listę klasyfikacji magazynu do zmiennej $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="b3969-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="b3969-211">Poniżej polecenia Pobierz klasyfikacji źródła do zmiennej i obiekt docelowy klasyfikacji $SourceClassificaion w zmiennej $TargetClassification.</span><span class="sxs-lookup"><span data-stu-id="b3969-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="b3969-212">Klasyfikacje źródłowym i docelowym może być dowolny element w tablicy.</span><span class="sxs-lookup"><span data-stu-id="b3969-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="b3969-213">Zapoznaj się z danymi wyjściowymi poniżej polecenie, aby ustalić indeksu źródłowej i docelowej klasyfikacje w tablicy $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="b3969-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="b3969-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object - FriendlyName właściwości, identyfikator | Formatowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="b3969-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="b3969-215">Poniżej polecenie cmdlet tworzy mapowanie między klasyfikacji źródłowego i docelowego klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="b3969-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="b3969-216">Krok 8. Włączanie ochrony dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="b3969-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="b3969-217">Po serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b3969-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="b3969-218">Aby włączyć ochronę, uruchom następujące polecenie, aby pobrać kontenera ochrony:</span><span class="sxs-lookup"><span data-stu-id="b3969-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="b3969-219">Pobierz jednostki ochrony (VM), uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3969-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="b3969-220">Włącz replikację dla maszyny Wirtualnej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3969-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="b3969-221">Testowanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b3969-221">Test your deployment</span></span>
<span data-ttu-id="b3969-222">Aby przetestować wdrożenie można uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania uwzględniający wiele maszyn wirtualnych i testować tryb failover planu.</span><span class="sxs-lookup"><span data-stu-id="b3969-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="b3969-223">Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej.</span><span class="sxs-lookup"><span data-stu-id="b3969-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="b3969-224">Plan odzyskiwania można utworzyć aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3969-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="b3969-225">Aby sprawdzić zakończenie operacji, postępuj zgodnie z instrukcjami [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="b3969-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="b3969-226">Wykonywanie próby przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="b3969-226">Run a test failover</span></span>
1. <span data-ttu-id="b3969-227">Uruchom poniżej polecenia cmdlet, aby pobrać maszyn wirtualnych do sieci maszyny Wirtualnej, z którą chcesz przetestować tryb failover.</span><span class="sxs-lookup"><span data-stu-id="b3969-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="b3969-228">Wykonaj test trybu failover maszyny wirtualnej, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3969-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="b3969-229">Wykonaj testowy tryb failover planu odzyskiwania, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3969-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="b3969-230">Realizacja planowanego trybu failover</span><span class="sxs-lookup"><span data-stu-id="b3969-230">Run a planned failover</span></span>
1. <span data-ttu-id="b3969-231">Wykonaj planowany tryb failover maszyny wirtualnej, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3969-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="b3969-232">Wykonaj planowany tryb failover planu odzyskiwania, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3969-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="b3969-233">Uruchom nieplanowanego trybu failover</span><span class="sxs-lookup"><span data-stu-id="b3969-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="b3969-234">Wykonaj nieplanowany tryb failover maszyny wirtualnej, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3969-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="b3969-235">2. Wykonaj nieplanowany tryb failover planu odzyskiwania, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3969-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="b3969-236"><a name=monitor></a>Monitorowanie aktywności</span><span class="sxs-lookup"><span data-stu-id="b3969-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="b3969-237">Użyj następujących poleceń, aby monitorować aktywność.</span><span class="sxs-lookup"><span data-stu-id="b3969-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="b3969-238">Należy pamiętać, że należy poczekać Between zadania do przetwarzania zakończyć.</span><span class="sxs-lookup"><span data-stu-id="b3969-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="b3969-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3969-239">Next steps</span></span>
<span data-ttu-id="b3969-240">[Dowiedz się więcej](/powershell/module/azurerm.recoveryservices.backup/#recovery) dotyczące usługi Azure Site Recovery za pomocą poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3969-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
