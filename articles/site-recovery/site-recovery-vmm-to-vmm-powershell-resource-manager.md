---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V w lokacji dodatkowej tooa VMM przy użyciu programu PowerShell (usługi Azure Resource Manager) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toodeploy usługi Azure Site Recovery tooorchestrate replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooa lokacja dodatkowa programu VMM przy użyciu programu PowerShell (Resource Manager)"
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
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="29f19-103">Replikowanie maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooa lokacja dodatkowa programu VMM przy użyciu programu PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="29f19-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29f19-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="29f19-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="29f19-105">Klasyczny portal</span><span class="sxs-lookup"><span data-stu-id="29f19-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="29f19-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29f19-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="29f19-107">Usługa Site Recovery tooAzure Zapraszamy!</span><span class="sxs-lookup"><span data-stu-id="29f19-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="29f19-108">W tym artykule należy użyć, jeśli tooreplicate lokalnych maszyn wirtualnych funkcji Hyper-V zarządzanych w lokacji dodatkowej tooa chmur programu System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="29f19-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="29f19-109">W tym artykule opisano, jak toouse PowerShell tooautomate typowych zadań należy tooperform podczas konfigurowania maszyny wirtualnej funkcji Hyper-V tooreplicate usługi Azure Site Recovery w chmurach VMM tooSystem Center chmur programu System Center VMM w lokacji dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="29f19-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="29f19-110">Hello artykuł zawiera wymagania wstępne dla scenariusza hello i pokazuje</span><span class="sxs-lookup"><span data-stu-id="29f19-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="29f19-111">Jak tooset się magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="29f19-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="29f19-112">Zainstaluj hello dostawcy usługi Azure Site Recovery na źródłowym serwerze programu VMM hello i hello docelowym serwerze VMM</span><span class="sxs-lookup"><span data-stu-id="29f19-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="29f19-113">Zarejestruj hello serwery VMM w magazynie hello</span><span class="sxs-lookup"><span data-stu-id="29f19-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="29f19-114">Skonfiguruj zasady replikacji dla hello chmury VMM.</span><span class="sxs-lookup"><span data-stu-id="29f19-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="29f19-115">ustawienia replikacji Hello hello zasady zostaną zastosowane tooall chronione maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="29f19-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="29f19-116">Włącz ochronę maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="29f19-117">Testowanie trybu failover hello maszyn wirtualnych, pojedynczo lub w ramach planu odzyskiwania toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="29f19-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="29f19-118">Wykonaj planowane lub nieplanowane przełączenie awaryjne maszyn wirtualnych, pojedynczo lub w ramach planu odzyskiwania toomake się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="29f19-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="29f19-119">Jeśli napotkasz problem ze skonfigurowaniem w tym scenariuszu Opublikuj swoje pytania na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="29f19-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="29f19-120">Platforma Azure ma dwa różne [modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md) związane z tworzeniem zasobów i pracą z nimi: Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="29f19-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="29f19-121">Azure ma dwa portale — klasyczny portal Azure obsługującym hello klasycznego modelu wdrażania hello i hello portalu Azure z obsługą oba modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="29f19-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="29f19-122">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="29f19-123">Lokalne wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="29f19-123">On-premises prerequisites</span></span>
<span data-ttu-id="29f19-124">Oto, co jest potrzebne w hello głównej i dodatkowej lokalnymi lokacji toodeploy tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="29f19-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="29f19-125">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="29f19-125">**Prerequisites**</span></span> | <span data-ttu-id="29f19-126">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="29f19-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="29f19-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="29f19-127">**VMM**</span></span> |<span data-ttu-id="29f19-128">Zaleca się wdrożyć serwer VMM w lokacji głównej hello a serwerem programu VMM w lokacji dodatkowej hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="29f19-129">Możesz również [replikacji między chmurami na jednym serwerze VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="29f19-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="29f19-130">toodo to będziesz potrzebować co najmniej dwóch chmur skonfigurowane na serwerze VMM hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="29f19-131">Serwery VMM powinna być uruchomiona co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="29f19-132">Każdy serwer VMM musi mieć jedną lub więcej chmur skonfigurowane i wszystkich chmur musi mieć zestawu profilu pojemności funkcji Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="29f19-133">Chmury muszą zawierać co najmniej jedną grupę hostów programu VMM.</span><span class="sxs-lookup"><span data-stu-id="29f19-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="29f19-134">Dowiedz się więcej o konfigurowaniu chmur VMM w [sieci szkieletowej chmury hello Konfigurowanie VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), i [wskazówki: tworzenie chmur prywatnych z programu System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="29f19-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="29f19-135">Program VMM serwery powinny mieć dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="29f19-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="29f19-136">**Funkcja Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="29f19-136">**Hyper-V**</span></span> |<span data-ttu-id="29f19-137">Serwery funkcji Hyper-V musi działać co najmniej Windows Server 2012 z rolą funkcji Hyper-V hello i mieć hello zainstalowane najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="29f19-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="29f19-138">Serwer funkcji Hyper-V powinien zawierać co najmniej jedną maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="29f19-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="29f19-139">Serwery hosta funkcji Hyper-V powinien znajdować się w grupach hostów w hello głównych i dodatkowych chmurach VMM.</span><span class="sxs-lookup"><span data-stu-id="29f19-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="29f19-140">Jeśli używasz funkcji Hyper-V w klastrze systemu Windows Server 2012 R2 należy zainstalować [zaktualizować 2961977](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="29f19-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="29f19-141">Jeśli korzystasz z funkcji Hyper-V w klastrze na Uwaga systemu Windows Server 2012 broker klastra nie jest tworzony automatycznie w przypadku statycznej klastra oparte na adresie IP.</span><span class="sxs-lookup"><span data-stu-id="29f19-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="29f19-142">Będziesz potrzebować brokera klastra hello tooconfigure ręcznie.</span><span class="sxs-lookup"><span data-stu-id="29f19-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="29f19-143">[Dowiedz się więcej](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="29f19-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="29f19-144">**Dostawca**</span><span class="sxs-lookup"><span data-stu-id="29f19-144">**Provider**</span></span> |<span data-ttu-id="29f19-145">Podczas wdrażania usługi Site Recovery należy zainstalować na serwerach VMM hello dostawcy usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29f19-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="29f19-146">Hello dostawca komunikuje się z usługą Site Recovery za pośrednictwem protokołu HTTPS 443 tooorchestrate replikacji.</span><span class="sxs-lookup"><span data-stu-id="29f19-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="29f19-147">Jest wykonywana replikacja danych między hello podstawowe i pomocnicze serwery funkcji Hyper-V za pośrednictwem hello sieci LAN lub połączenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="29f19-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="29f19-148">Hello dostawca uruchomiony na serwerze VMM hello musi uzyskać dostępu do adresów URL toothese: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="29f19-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="29f19-149">Ponadto Zezwalaj na komunikację zapory z toohello serwery VMM hello [zakresy IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) i umożliwić hello protokołu HTTPS (port 443).</span><span class="sxs-lookup"><span data-stu-id="29f19-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="29f19-150">Wymagania wstępne związane z mapowaniem sieci</span><span class="sxs-lookup"><span data-stu-id="29f19-150">Network mapping prerequisites</span></span>
<span data-ttu-id="29f19-151">Mapowanie sieci działa między sieciami maszyn wirtualnych VMM na powitania podstawowym i pomocniczym serwerze programu VMM do:</span><span class="sxs-lookup"><span data-stu-id="29f19-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="29f19-152">Optymalnie umieścić po pracy awaryjnej maszyn wirtualnych repliki dodatkowej hosty funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="29f19-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="29f19-153">Połączenia sieci VM tooappropriate maszyn wirtualnych repliki.</span><span class="sxs-lookup"><span data-stu-id="29f19-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="29f19-154">Jeśli nie zostanie skonfigurowana sieć mapowania repliki maszyn wirtualnych nie będą tooany połączonych sieci po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="29f19-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="29f19-155">Jeśli chcesz, aby tooset sieć mapowania podczas odzyskiwania lokacji wdrożenia w tym miejscu to co jest potrzebne:</span><span class="sxs-lookup"><span data-stu-id="29f19-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="29f19-156">Upewnij się, że maszyny wirtualne w źródle powitania serwera hosta funkcji Hyper-V są tooa połączonych sieci maszyny Wirtualnej VMM.</span><span class="sxs-lookup"><span data-stu-id="29f19-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="29f19-157">Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="29f19-158">Sprawdź, czy hello dodatkowej chmury, które będzie używane do odzyskiwania ma skonfigurowane odpowiednie sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29f19-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="29f19-159">Ta sieć maszyn wirtualnych powinny być tooa połączone sieci logicznej, która ma powiązanego z chmurą dodatkowej hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="29f19-160">Dowiedz się więcej o konfigurowaniu sieci w programie VMM w hello poniżej artykułów</span><span class="sxs-lookup"><span data-stu-id="29f19-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="29f19-161">Jak tooconfigure sieci logicznych w programie VMM</span><span class="sxs-lookup"><span data-stu-id="29f19-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="29f19-162">Jak tooconfigure maszyny Wirtualnej sieci i bram w programie VMM</span><span class="sxs-lookup"><span data-stu-id="29f19-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="29f19-163">[Dowiedz się więcej](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) o tym, jak działa mapowanie sieci.</span><span class="sxs-lookup"><span data-stu-id="29f19-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="29f19-164">Wymagania wstępne programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="29f19-164">PowerShell prerequisites</span></span>
<span data-ttu-id="29f19-165">Upewnij się, że masz toogo gotowy programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29f19-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="29f19-166">Jeśli korzystasz już z programu PowerShell, potrzebujesz tooupgrade tooversion 0.8.10 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="29f19-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="29f19-167">Aby uzyskać informacje o konfigurowaniu programu PowerShell, zobacz hello [prowadzą tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="29f19-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="29f19-168">Po należy skonfigurować i skonfigurowaniu programu PowerShell można wyświetlić wszystkie dostępne polecenia cmdlet hello hello usługi [tutaj](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29f19-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="29f19-169">toolearn o porad ułatwiających przy użyciu poleceń cmdlet hello, takich jak jak wartości parametru, dane wejściowe i dane wyjściowe są zazwyczaj obsługiwane w programie Azure PowerShell, zobacz hello [przewodnik tooget uruchomiona za pomocą poleceń cmdlet Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="29f19-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="29f19-170">Krok 1: Ustaw hello subskrypcji</span><span class="sxs-lookup"><span data-stu-id="29f19-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="29f19-171">Z programu Azure powershell tooyour logowania konta platformy Azure: za pomocą następującego polecenia cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="29f19-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="29f19-172">Pobierz listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="29f19-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="29f19-173">To wyświetla również hello subscriptionIDs dla każdego hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="29f19-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="29f19-174">Zanotuj identyfikator subskrypcji hello hello subskrypcji, w którym chcesz magazynu usług odzyskiwania hello toocreate</span><span class="sxs-lookup"><span data-stu-id="29f19-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="29f19-175">Ustaw hello subskrypcji, w których hello magazynu usług odzyskiwania jest utworzony, podając identyfikator subskrypcji hello toobe</span><span class="sxs-lookup"><span data-stu-id="29f19-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="29f19-176">Krok 2. Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="29f19-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="29f19-177">Tworzenie grupy zasobów platformy Azure Resource Manager, jeśli nie masz już</span><span class="sxs-lookup"><span data-stu-id="29f19-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="29f19-178">Utwórz nowy magazyn usług odzyskiwania i zapisać hello utworzony obiekt magazynu ASR w zmiennej (zostanie później użyty).</span><span class="sxs-lookup"><span data-stu-id="29f19-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="29f19-179">Można również pobierać hello ASR magazynu obiektu post tworzenia przy użyciu polecenia cmdlet Get-AzureRMRecoveryServicesVault hello:-</span><span class="sxs-lookup"><span data-stu-id="29f19-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="29f19-180">Krok 3: Ustaw hello kontekst magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="29f19-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="29f19-181">Jeśli masz już utworzony magazyn, należy uruchomić hello poniżej polecenia tooget hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="29f19-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="29f19-182">Ustaw kontekst magazynu hello uruchamiając hello poniżej polecenia.</span><span class="sxs-lookup"><span data-stu-id="29f19-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="29f19-183">Krok 4: Instalowanie hello dostawcy usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="29f19-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="29f19-184">Na maszynie VMM hello należy utworzyć katalog, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="29f19-185">Wyodrębnij pliki hello przy użyciu dostawcy hello pobrane, uruchamiając następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="29f19-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="29f19-186">Zainstaluj dostawcę hello przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29f19-186">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="29f19-187">Poczekaj na powitania toofinish instalacji.</span><span class="sxs-lookup"><span data-stu-id="29f19-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="29f19-188">Zarejestruj serwer hello w magazynie hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29f19-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="29f19-189">Krok 5: Utwórz i Skojarz zasady replikacji</span><span class="sxs-lookup"><span data-stu-id="29f19-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="29f19-190">Utwórz zasady replikacji funkcji Hyper-V 2012 R2, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="29f19-191">Witaj chmury VMM może zawierać hosty funkcji Hyper-V z różnymi wersjami systemu Windows Server (jak wspomniano w wymagania wstępne funkcji Hyper-V hello), ale zasady replikacji hello jest właściwego dla wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="29f19-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="29f19-192">Jeśli masz różnych hostach z systemem w wersji systemów operacyjnych, następnie utwórz zasady replikacji osobne dla każdego typu wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="29f19-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="29f19-193">Aby uzyskać np: Jeśli masz pięć hostów z uruchomionym systemem Windows 2012 serwerów i trzech w systemie Windows Server 2012 R2, należy utworzyć dwa zasady replikacji — po jednej dla każdego typu wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="29f19-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="29f19-194">Pobierz kontener ochronę podstawową hello (podstawowy chmury VMM) i odzyskiwania kontenera ochrony (odzyskiwania chmury VMM), uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="29f19-195">Pobierania zasad hello utworzonego w kroku 1 przy użyciu przyjaznej nazwy zasady hello hello</span><span class="sxs-lookup"><span data-stu-id="29f19-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="29f19-196">Uruchom skojarzenie hello hello kontenera ochrony (w chmurze VMM) z zasadami replikacji hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="29f19-197">Poczekaj, aż toocomplete zadania skojarzenia zasad hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="29f19-198">Możesz sprawdzić, jeśli zadania hello zakończone przy użyciu powitania po fragment programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29f19-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="29f19-199">Po zakończeniu przetwarzania zadania hello, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="29f19-200">toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="29f19-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="29f19-201">Krok 6: Skonfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="29f19-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="29f19-202">Witaj pierwsze polecenie pobiera serwerów hello bieżący magazyn Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29f19-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="29f19-203">polecenie Hello przechowuje hello serwerów Microsoft Azure Site Recovery w hello $Servers tablicy zmiennej.</span><span class="sxs-lookup"><span data-stu-id="29f19-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="29f19-204">Witaj poniżej polecenia Pobierz sieć odzyskiwania lokacji hello hello źródłowym serwerze programu VMM i hello docelowym serwerze VMM.</span><span class="sxs-lookup"><span data-stu-id="29f19-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="29f19-205">Witaj źródłowym serwerze programu VMM można Witaj, pierwszy lub hello drugi hello w jednym serwerów tablicy.</span><span class="sxs-lookup"><span data-stu-id="29f19-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="29f19-206">Sprawdź nazwy hello hello serwerów programu VMM i odpowiednio uzyskać hello sieci</span><span class="sxs-lookup"><span data-stu-id="29f19-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="29f19-207">polecenie cmdlet końcowego Hello tworzy mapowanie między hello sieci podstawowej i hello odzyskiwania sieci.</span><span class="sxs-lookup"><span data-stu-id="29f19-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="29f19-208">polecenia cmdlet Hello określa hello sieci podstawowej jako pierwszy element hello $PrimaryNetworks i hello sieci odzyskiwania jako pierwszy element $RecoveryNetworks hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="29f19-209">Krok 7: Konfigurowanie mapowania magazynu</span><span class="sxs-lookup"><span data-stu-id="29f19-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="29f19-210">Witaj poniżej polecenie pobiera hello Lista klasyfikacji magazynu do zmiennej $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="29f19-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="29f19-211">Hello poniżej polecenia pobrania hello źródła klasyfikacji w zmiennej $SourceClassificaion i klasyfikacji docelowego w zmiennej $TargetClassification.</span><span class="sxs-lookup"><span data-stu-id="29f19-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="29f19-212">klasyfikacje Hello źródłowym i docelowym może być dowolny element w tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="29f19-213">Zobacz dane wyjściowe toohello hello poniżej indeks hello toofigure polecenia źródłowa i docelowa klasyfikacji $storageclassifications tablicy.</span><span class="sxs-lookup"><span data-stu-id="29f19-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="29f19-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object - FriendlyName właściwości, identyfikator | Formatowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="29f19-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="29f19-215">Hello poniżej polecenie cmdlet tworzy mapowanie między hello źródła klasyfikacji i hello docelowy klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="29f19-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="29f19-216">Krok 8. Włączanie ochrony dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="29f19-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="29f19-217">Po hello serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="29f19-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="29f19-218">Ochrona tooenable hello uruchom następujące polecenia kontenera ochrony hello tooget:</span><span class="sxs-lookup"><span data-stu-id="29f19-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="29f19-219">Pobierz jednostki ochrony hello (VM), uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="29f19-220">Włącz replikację hello maszyny Wirtualnej, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="29f19-221">Testowanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="29f19-221">Test your deployment</span></span>
<span data-ttu-id="29f19-222">Planowanie wdrożenia możesz uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania składające się z wielu maszyn wirtualnych i uruchomić test trybu failover dla hello tootest.</span><span class="sxs-lookup"><span data-stu-id="29f19-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="29f19-223">Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej.</span><span class="sxs-lookup"><span data-stu-id="29f19-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="29f19-224">Plan odzyskiwania można utworzyć aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29f19-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="29f19-225">toocheck hello ukończenia operacji hello, wykonaj kroki hello w [monitorowanie aktywności](#monitor).</span><span class="sxs-lookup"><span data-stu-id="29f19-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="29f19-226">Wykonywanie próby przejścia w tryb failover</span><span class="sxs-lookup"><span data-stu-id="29f19-226">Run a test failover</span></span>
1. <span data-ttu-id="29f19-227">Uruchom hello poniżej poleceń cmdlet tooget hello maszyny Wirtualnej sieci toowhich ma tootest trybu failover do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="29f19-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="29f19-228">Wykonaj test trybu failover maszyny wirtualnej, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="29f19-229">Wykonaj test trybu failover planu odzyskiwania, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="29f19-230">Realizacja planowanego trybu failover</span><span class="sxs-lookup"><span data-stu-id="29f19-230">Run a planned failover</span></span>
1. <span data-ttu-id="29f19-231">Wykonaj planowany tryb failover maszyny wirtualnej, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="29f19-232">Planowany tryb failover planu odzyskiwania należy wykonać następujący hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="29f19-233">Uruchom nieplanowanego trybu failover</span><span class="sxs-lookup"><span data-stu-id="29f19-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="29f19-234">Wykonaj nieplanowany tryb failover maszyny wirtualnej, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="29f19-235">2. Wykonaj nieplanowany tryb failover planu odzyskiwania, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29f19-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="29f19-236"><a name=monitor></a>Monitorowanie aktywności</span><span class="sxs-lookup"><span data-stu-id="29f19-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="29f19-237">Witaj Użyj następującego polecenia toomonitor hello działania.</span><span class="sxs-lookup"><span data-stu-id="29f19-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="29f19-238">Należy pamiętać, że masz toowait Between zadania hello toofinish przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="29f19-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="29f19-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29f19-239">Next steps</span></span>
<span data-ttu-id="29f19-240">[Dowiedz się więcej](/powershell/module/azurerm.recoveryservices.backup/#recovery) dotyczące usługi Azure Site Recovery za pomocą poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29f19-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
