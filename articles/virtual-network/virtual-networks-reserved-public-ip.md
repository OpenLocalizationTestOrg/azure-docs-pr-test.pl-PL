---
title: "aaaManage Azure zastrzeżonych adresów IP (klasyczne) - PowerShell | Dokumentacja firmy Microsoft"
description: "Zrozumienie zastrzeżone adresy IP (klasyczne) i w jaki sposób toomanage ich przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="e0590-103">Zastrzeżone adresy IP (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="e0590-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0590-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e0590-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="e0590-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0590-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="e0590-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e0590-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="e0590-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="e0590-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="e0590-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e0590-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="e0590-109">Adresy IP na platformie Azure można podzielić na dwie kategorie: dynamiczne i zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="e0590-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="e0590-110">Publiczne adresy IP, zarządzane przez usługę Azure są dynamiczne domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e0590-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="e0590-111">Czy oznacza, że hello adres IP używany dla określonej chmury usługi (VIP) lub tooaccess maszyny Wirtualnej lub bezpośrednio wystąpienia roli (ILPIP) może zostać zmieniony z tootime czasu, gdy zasoby są zamknięte lub zatrzymana (cofnięciu przydziału).</span><span class="sxs-lookup"><span data-stu-id="e0590-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="e0590-112">adresy IP tooprevent zmianę, można zastrzec adres IP.</span><span class="sxs-lookup"><span data-stu-id="e0590-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="e0590-113">Zastrzeżonych adresów IP może służyć wyłącznie jako adresu VIP, zapewniając tego hello adresu IP dla usługi w chmurze hello pozostaje hello takie same, nawet jeśli zasoby są zamknięte lub zatrzymana (cofnięciu przydziału).</span><span class="sxs-lookup"><span data-stu-id="e0590-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="e0590-114">Ponadto można przekonwertować istniejące dynamicznych adresów IP używany jako adres IP tooa zarezerwowane wirtualne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="e0590-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0590-115">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e0590-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e0590-116">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e0590-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="e0590-117">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0590-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e0590-118">Dowiedz się, jak hello tooreserve statyczny publiczny adres IP przy użyciu [modelu wdrażania usługi Resource Manager](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e0590-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="e0590-119">adresy toolearn więcej informacji na temat adresu IP na platformie Azure, przeczytaj hello [adresów IP](virtual-network-ip-addresses-overview-classic.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e0590-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="e0590-120">Jeśli potrzebujesz zastrzeżony adres IP?</span><span class="sxs-lookup"><span data-stu-id="e0590-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="e0590-121">**Ma tooensure, który hello IP jest zarezerwowana w ramach subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="e0590-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="e0590-122">Jeśli chcesz tooreserve adresu IP, który nie jest zwalniany z subskrypcją w żadnym przypadku należy używać zastrzeżonego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e0590-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="e0590-123">**Ma toostay Twojego adresu IP z usługi w chmurze, nawet w poprzek zatrzymana lub alokację stanu (VM)**.</span><span class="sxs-lookup"><span data-stu-id="e0590-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="e0590-124">Jeśli chcesz, aby Twoje toobe usługi dostępne za pośrednictwem adresu IP, który nie ulega zmianie, nawet w przypadku maszyn wirtualnych w hello w chmurze usługi są zamknięte lub Zatrzymaj (cofnięciu przydziału).</span><span class="sxs-lookup"><span data-stu-id="e0590-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="e0590-125">**Ma tooensure, że ruch wychodzący z platformy Azure używa przewidywalną adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="e0590-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="e0590-126">Może być lokalnymi skonfigurowano zaporę tooallow tylko ruchu z określonych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e0590-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="e0590-127">Przez zarezerwowanie adresów IP, wiesz hello źródłowy adres IP adresów i nie trzeba tooupdate reguły zapory powodu tooan zmiany adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e0590-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="e0590-128">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="e0590-128">FAQ</span></span>
1. <span data-ttu-id="e0590-129">Dla wszystkich usług platformy Azure można używać zastrzeżonego adresu IP?</span><span class="sxs-lookup"><span data-stu-id="e0590-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="e0590-130">Nie.</span><span class="sxs-lookup"><span data-stu-id="e0590-130">No.</span></span> <span data-ttu-id="e0590-131">Zastrzeżonych adresów IP można używać tylko dla maszyn wirtualnych i role wystąpienia usługi w chmurze za pośrednictwem adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="e0590-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="e0590-132">Jak wiele zastrzeżonych adresów IP może mieć?</span><span class="sxs-lookup"><span data-stu-id="e0590-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="e0590-133">Aby uzyskać więcej informacji, zobacz hello [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e0590-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="e0590-134">Dla zarezerwowanych adresów IP jest opłatę?</span><span class="sxs-lookup"><span data-stu-id="e0590-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="e0590-135">Czasami.</span><span class="sxs-lookup"><span data-stu-id="e0590-135">Sometimes.</span></span> <span data-ttu-id="e0590-136">Aby uzyskać szczegółowe informacje o cenach, zobacz hello [zastrzeżonego adresu IP Address szczegóły cennika](http://go.microsoft.com/fwlink/?LinkID=398482) strony.</span><span class="sxs-lookup"><span data-stu-id="e0590-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="e0590-137">Jak zastrzeżenia adresu IP?</span><span class="sxs-lookup"><span data-stu-id="e0590-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="e0590-138">Korzystając z programu PowerShell, hello [interfejsu API REST zarządzania Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), lub hello [portalu Azure](https://portal.azure.com) tooreserve adresu IP w regionie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e0590-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="e0590-139">Zastrzeżony adres IP jest skojarzony tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e0590-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="e0590-140">Czy można używać zastrzeżonego adresu IP z sieci oparte na grupach koligacji wirtualnych?</span><span class="sxs-lookup"><span data-stu-id="e0590-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="e0590-141">Nie.</span><span class="sxs-lookup"><span data-stu-id="e0590-141">No.</span></span> <span data-ttu-id="e0590-142">Zastrzeżonych adresów IP są obsługiwane tylko w regionalnych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e0590-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="e0590-143">Zastrzeżonych adresów IP nie są obsługiwane dla sieci wirtualnych, które są skojarzone z grup koligacji.</span><span class="sxs-lookup"><span data-stu-id="e0590-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="e0590-144">Aby uzyskać więcej informacji o sposobie kojarzenia sieci wirtualnej z region lub grupę koligacji, zobacz hello [o sieci regionalnych wirtualnych i grup koligacji](virtual-networks-migrate-to-regional-vnet.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e0590-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="e0590-145">Zarządzanie zarezerwowanych adresów VIP</span><span class="sxs-lookup"><span data-stu-id="e0590-145">Manage reserved VIPs</span></span>

<span data-ttu-id="e0590-146">Upewnij się, zostanie zainstalowany i skonfigurowany programu PowerShell, wykonując kroki hello hello [Instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e0590-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="e0590-147">Przed użyciem zastrzeżonych adresów IP, należy dodać tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e0590-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="e0590-148">toocreate zastrzeżony adres IP z puli hello publicznego adresu IP, adresy dostępne w hello *środkowe stany USA* lokalizacji, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e0590-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="e0590-149">Zwróć uwagę, że nie można określić adresu IP, jakie są zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="e0590-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="e0590-150">tooview adresów IP, które są zarezerwowane w ramach subskrypcji, uruchom następujące polecenia programu PowerShell hello i zwróć uwagę, wartości hello *nazwa zastrzeżonego adresu IP* i *adres*:</span><span class="sxs-lookup"><span data-stu-id="e0590-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="e0590-151">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e0590-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="e0590-152">Po utworzeniu zastrzeżonego adresu IP przy użyciu programu PowerShell nie można określić IP hello zarezerwowanych zasobów grupy toocreate w.</span><span class="sxs-lookup"><span data-stu-id="e0590-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="e0590-153">Azure miejsca go do grupy zasobów o nazwie *sieci domyślne* automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e0590-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="e0590-154">Jeśli utworzysz hello zastrzeżone IP przy użyciu hello [portalu Azure](http://portal.azure.com), można określić dowolną grupę zasobów, możesz wybrać.</span><span class="sxs-lookup"><span data-stu-id="e0590-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="e0590-155">Jeśli utworzysz IP hello zarezerwowane w grupie zasobów innych niż *sieci domyślne* jednak zawsze, gdy odwołanie hello zastrzeżony adres IP za pomocą polecenia takie jak `Get-AzureReservedIP` i `Remove-AzureReservedIP`, musi odwoływać się nazwy hello *Zarezerwowana nazwa grupy zasobów ip — Nazwa grupy*.</span><span class="sxs-lookup"><span data-stu-id="e0590-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="e0590-156">Na przykład w przypadku utworzenia zastrzeżony adres IP o nazwie *myReservedIP* w grupie zasobów o nazwie *myResourceGroup*, musi odwoływać się nazwy hello IP hello zarezerwowane jako *myResourceGroup grupy myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="e0590-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="e0590-157">Gdy adres IP jest zarezerwowany, pozostaje subskrypcji skojarzone tooyour dopóki nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="e0590-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="e0590-158">toodelete zastrzeżonego adresu IP hello uruchom następujące polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e0590-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="e0590-159">Zarezerwowania adresu IP hello istniejącą usługę w chmurze</span><span class="sxs-lookup"><span data-stu-id="e0590-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="e0590-160">Można zastrzec adresu IP hello istniejącej usługi w chmurze, dodając hello `-ServiceName` parametru.</span><span class="sxs-lookup"><span data-stu-id="e0590-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="e0590-161">adres IP hello tooreserve usługi w chmurze *TestService* w hello *środkowe stany USA* lokalizacji, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="e0590-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="e0590-162">Skojarzyć zastrzeżonego adresu IP tooa nową usługę w chmurze</span><span class="sxs-lookup"><span data-stu-id="e0590-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="e0590-163">Witaj poniższy skrypt tworzy nowy zastrzeżony adres IP, a następnie kojarzy ją tooa nową usługę w chmurze o nazwie *TestService*.</span><span class="sxs-lookup"><span data-stu-id="e0590-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="e0590-164">Po utworzeniu zastrzeżone toouse IP z usługi w chmurze, nadal odwołanie toohello maszyny Wirtualnej za pomocą *VIP:&lt;numer portu >* dla komunikacji przychodzącej.</span><span class="sxs-lookup"><span data-stu-id="e0590-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="e0590-165">Rezerwacja adresu IP oznacza to, że można połączyć bezpośrednio toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0590-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="e0590-166">Witaj zastrzeżony adres IP jest przypisywany toohello chmury usługi hello, że maszyna wirtualna została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="e0590-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="e0590-167">Jeśli chcesz tooa tooconnect maszynę Wirtualną za IP bezpośrednio, masz tooconfigure publicznego adresu IP poziomie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e0590-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="e0590-168">Publiczny adres IP poziomie wystąpienia jest typu publicznego adresu IP (nazywane ILPIP) przypisane bezpośrednio tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0590-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="e0590-169">Nie można zarezerwować.</span><span class="sxs-lookup"><span data-stu-id="e0590-169">It cannot be reserved.</span></span> <span data-ttu-id="e0590-170">Aby uzyskać więcej informacji, przeczytaj hello [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e0590-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="e0590-171">Usuwanie zastrzeżonego adresu IP z wykonywanego wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e0590-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="e0590-172">zastrzeżony adres IP tooremove dodane tooa nową usługę w chmurze, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="e0590-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="e0590-173">Usuwanie zastrzeżonego adresu IP z wykonywanego wdrożenia nie powoduje usunięcia rezerwacji hello z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e0590-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="e0590-174">Po prostu powoduje zwolnienie hello toobe IP używany przez inny zasób w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e0590-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="e0590-175">Skojarzyć zastrzeżonego tooa IP uruchamiania wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e0590-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="e0590-176">Witaj następujące polecenia tworzenia usługi w chmurze o nazwie *TestService2* z nowej maszyny Wirtualnej o nazwie *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="e0590-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="e0590-177">istniejące Hello zastrzeżony adres IP o nazwie *MyReservedIP* jest następnie toohello skojarzona usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e0590-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="e0590-178">Skojarzyć zastrzeżonego adresu IP tooa usługą w chmurze przy użyciu pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="e0590-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="e0590-179">Można również skojarzyć zastrzeżonego adresu IP tooa usługą w chmurze przy użyciu pliku konfiguracji (CSCFG) usługi.</span><span class="sxs-lookup"><span data-stu-id="e0590-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="e0590-180">Witaj następujące przykładowe xml pokazuje sposób tooconfigure toouse usługi chmury zarezerwowanych adresów VIP o nazwie *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="e0590-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="e0590-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0590-181">Next steps</span></span>
* <span data-ttu-id="e0590-182">Zrozumienie sposobu [adresowanie IP](virtual-network-ip-addresses-overview-classic.md) działa w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e0590-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="e0590-183">Dowiedz się więcej o [prywatne adresy IP zarezerwowane](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="e0590-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="e0590-184">Dowiedz się więcej o [adresy IP publicznego poziom wystąpienia (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="e0590-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

