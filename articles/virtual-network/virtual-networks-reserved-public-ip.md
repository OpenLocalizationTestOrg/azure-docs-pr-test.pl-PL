---
title: "Zarządzanie Azure zastrzeżone adresy IP (klasyczne) - PowerShell | Dokumentacja firmy Microsoft"
description: "Zrozumienie zastrzeżone adresy IP (klasyczne) i jak nimi zarządzać przy użyciu programu PowerShell."
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
ms.openlocfilehash: 5e9c83cebec96c6bc8afd53b0c637d7af899746f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="37c29-103">Zastrzeżone adresy IP (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="37c29-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="37c29-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="37c29-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="37c29-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37c29-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="37c29-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="37c29-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="37c29-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="37c29-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="37c29-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="37c29-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="37c29-109">Adresy IP na platformie Azure można podzielić na dwie kategorie: dynamiczne i zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="37c29-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="37c29-110">Publiczne adresy IP, zarządzane przez usługę Azure są dynamiczne domyślnie.</span><span class="sxs-lookup"><span data-stu-id="37c29-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="37c29-111">Oznacza to, że adres IP używany dla określonej chmury usługi (VIP) lub uzyskać dostępu do maszyny Wirtualnej lub bezpośrednio wystąpienia roli (ILPIP) mogą ulec zmianie od czasu do czasu, po zasoby są zamknięte lub zatrzymana (cofnięciu przydziału).</span><span class="sxs-lookup"><span data-stu-id="37c29-111">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="37c29-112">Aby uniemożliwić zmianę adresów IP, można zastrzec adresu IP.</span><span class="sxs-lookup"><span data-stu-id="37c29-112">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="37c29-113">Zastrzeżonych adresów IP może służyć wyłącznie jako adresu VIP, zapewniając, że adres IP dla usługi w chmurze jest taka sama, nawet jeśli zasoby są zamknięte lub zatrzymana (cofnięciu przydziału).</span><span class="sxs-lookup"><span data-stu-id="37c29-113">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="37c29-114">Ponadto można przekonwertować istniejące dynamiczne adresy IP używane jako adresu VIP do zastrzeżonego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="37c29-114">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37c29-115">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="37c29-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="37c29-116">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="37c29-116">This article covers using the classic deployment model.</span></span> <span data-ttu-id="37c29-117">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="37c29-117">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="37c29-118">Dowiedz się, jak Zarezerwuj statyczny publiczny adres IP przy użyciu [modelu wdrażania usługi Resource Manager](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="37c29-118">Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="37c29-119">Aby dowiedzieć się więcej na temat adresów IP na platformie Azure, przeczytaj [adresów IP](virtual-network-ip-addresses-overview-classic.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="37c29-119">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="37c29-120">Jeśli potrzebujesz zastrzeżony adres IP?</span><span class="sxs-lookup"><span data-stu-id="37c29-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="37c29-121">**Aby upewnić się, że adres IP jest zarezerwowana w ramach subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="37c29-121">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="37c29-122">Jeśli chcesz zastrzeżenia adresu IP, który nie jest zwalniany z subskrypcją w żadnym przypadku należy używać zastrzeżonego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="37c29-122">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="37c29-123">**Ma IP pozostanie z usługi w chmurze nawet w poprzek zatrzymana lub alokację stanu (VM)**.</span><span class="sxs-lookup"><span data-stu-id="37c29-123">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="37c29-124">Jeśli chcesz, aby usługi można uzyskać dostęp przy użyciu adresu IP który nie powoduje zmiany, nawet wtedy, gdy maszyny wirtualne w usłudze w chmurze są zamknięte lub zatrzymać (cofnięciu przydziału).</span><span class="sxs-lookup"><span data-stu-id="37c29-124">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="37c29-125">**Aby zagwarantować, że ruch wychodzący z platformy Azure używał przewidywalną adres IP**.</span><span class="sxs-lookup"><span data-stu-id="37c29-125">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="37c29-126">Może być Zapora lokalnymi skonfigurowany tak, aby zezwolić tylko na ruch z określonych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="37c29-126">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="37c29-127">Przez zarezerwowanie adresów IP, które znasz źródłowy adres IP i nie trzeba zaktualizować reguł zapory z powodu zmiany adresu IP.</span><span class="sxs-lookup"><span data-stu-id="37c29-127">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="37c29-128">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="37c29-128">FAQ</span></span>
1. <span data-ttu-id="37c29-129">Dla wszystkich usług platformy Azure można używać zastrzeżonego adresu IP?</span><span class="sxs-lookup"><span data-stu-id="37c29-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="37c29-130">Nie.</span><span class="sxs-lookup"><span data-stu-id="37c29-130">No.</span></span> <span data-ttu-id="37c29-131">Zastrzeżonych adresów IP można używać tylko dla maszyn wirtualnych i role wystąpienia usługi w chmurze za pośrednictwem adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="37c29-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="37c29-132">Jak wiele zastrzeżonych adresów IP może mieć?</span><span class="sxs-lookup"><span data-stu-id="37c29-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="37c29-133">Aby uzyskać więcej informacji, zobacz [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="37c29-133">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="37c29-134">Dla zarezerwowanych adresów IP jest opłatę?</span><span class="sxs-lookup"><span data-stu-id="37c29-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="37c29-135">Czasami.</span><span class="sxs-lookup"><span data-stu-id="37c29-135">Sometimes.</span></span> <span data-ttu-id="37c29-136">Aby uzyskać szczegółowe informacje o cenach, zobacz [zastrzeżonego adresu IP Address szczegóły cennika](http://go.microsoft.com/fwlink/?LinkID=398482) strony.</span><span class="sxs-lookup"><span data-stu-id="37c29-136">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="37c29-137">Jak zastrzeżenia adresu IP?</span><span class="sxs-lookup"><span data-stu-id="37c29-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="37c29-138">Korzystając z programu PowerShell, [interfejsu API REST zarządzania Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), lub [portalu Azure](https://portal.azure.com) do zarezerwowania adresu IP w regionie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="37c29-138">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="37c29-139">Zastrzeżony adres IP jest skojarzony z subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="37c29-139">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="37c29-140">Czy można używać zastrzeżonego adresu IP z sieci oparte na grupach koligacji wirtualnych?</span><span class="sxs-lookup"><span data-stu-id="37c29-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="37c29-141">Nie.</span><span class="sxs-lookup"><span data-stu-id="37c29-141">No.</span></span> <span data-ttu-id="37c29-142">Zastrzeżonych adresów IP są obsługiwane tylko w regionalnych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="37c29-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="37c29-143">Zastrzeżonych adresów IP nie są obsługiwane dla sieci wirtualnych, które są skojarzone z grup koligacji.</span><span class="sxs-lookup"><span data-stu-id="37c29-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="37c29-144">Aby uzyskać więcej informacji o sposobie kojarzenia sieci wirtualnej z region lub grupę koligacji, zobacz [o sieci regionalnych wirtualnych i grup koligacji](virtual-networks-migrate-to-regional-vnet.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="37c29-144">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="37c29-145">Zarządzanie zarezerwowanych adresów VIP</span><span class="sxs-lookup"><span data-stu-id="37c29-145">Manage reserved VIPs</span></span>

<span data-ttu-id="37c29-146">Upewnij się, zostanie zainstalowany i skonfigurowany programu PowerShell, wykonując kroki opisane w [Instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="37c29-146">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="37c29-147">Przed użyciem zastrzeżonych adresów IP, należy ją dodać do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="37c29-147">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="37c29-148">Aby utworzyć zastrzeżonego adresu IP z puli publicznych adresów IP dostępne w *środkowe stany USA* lokalizacji, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="37c29-148">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="37c29-149">Zwróć uwagę, że nie można określić adresu IP, jakie są zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="37c29-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="37c29-150">Aby wyświetlić adresy IP, które są zastrzeżone w ramach subskrypcji, uruchom następujące polecenie programu PowerShell i zwróć uwagę na wartości dla *nazwa zastrzeżonego adresu IP* i *adres*:</span><span class="sxs-lookup"><span data-stu-id="37c29-150">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="37c29-151">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="37c29-151">Expected output:</span></span>

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
><span data-ttu-id="37c29-152">Po utworzeniu zastrzeżonego adresu IP przy użyciu programu PowerShell nie można określić grupę zasobów, aby utworzyć zastrzeżonego adresu IP w.</span><span class="sxs-lookup"><span data-stu-id="37c29-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in.</span></span> <span data-ttu-id="37c29-153">Azure miejsca go do grupy zasobów o nazwie *sieci domyślne* automatycznie.</span><span class="sxs-lookup"><span data-stu-id="37c29-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="37c29-154">Jeśli utworzysz zastrzeżonego adresu IP za pomocą [portalu Azure](http://portal.azure.com), można określić dowolną grupę zasobów, możesz wybrać.</span><span class="sxs-lookup"><span data-stu-id="37c29-154">If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="37c29-155">Jeśli utworzysz zastrzeżonego adresu IP w grupie zasobów innych niż *sieci domyślne* jednak zawsze, gdy odwołanie zastrzeżonego adresu IP za pomocą polecenia takie jak `Get-AzureReservedIP` i `Remove-AzureReservedIP`, musi odwoływać się do nazwy  *Zarezerwowana nazwa grupy zasobów ip — Nazwa grupy*.</span><span class="sxs-lookup"><span data-stu-id="37c29-155">If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="37c29-156">Na przykład w przypadku utworzenia zastrzeżony adres IP o nazwie *myReservedIP* w grupie zasobów o nazwie *myResourceGroup*, musi odwoływać się do nazwy zastrzeżonego adresu IP jako *myResourceGroup grupy myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="37c29-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="37c29-157">Gdy adres IP jest zarezerwowany, pozostaje skojarzona z subskrypcją dopóki nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="37c29-157">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="37c29-158">Aby usunąć zastrzeżonego adresu IP, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37c29-158">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="37c29-159">Rezerwacja adresu IP istniejącej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="37c29-159">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="37c29-160">Adres IP istniejącej usługi w chmurze może zarezerwować przez dodanie `-ServiceName` parametru.</span><span class="sxs-lookup"><span data-stu-id="37c29-160">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="37c29-161">Do zarezerwowania adresu IP usługi w chmurze *TestService* w *środkowe stany USA* lokalizacji, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37c29-161">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="37c29-162">Skojarzyć zastrzeżonego adresu IP do nowej usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="37c29-162">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="37c29-163">Poniższy skrypt tworzy nowy zastrzeżony adres IP, a następnie kojarzy ją do nowej usługi w chmurze o nazwie *TestService*.</span><span class="sxs-lookup"><span data-stu-id="37c29-163">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="37c29-164">Podczas tworzenia zastrzeżonego adresu IP do użycia z usługą w chmurze, nadal odwołujesz się do maszyny Wirtualnej za pomocą *VIP:&lt;numer portu >* dla komunikacji przychodzącej.</span><span class="sxs-lookup"><span data-stu-id="37c29-164">When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="37c29-165">Rezerwacja adresu IP oznacza to, że można połączyć się z maszyną Wirtualną bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="37c29-165">Reserving an IP does not mean you can connect to the VM directly.</span></span> <span data-ttu-id="37c29-166">Zastrzeżony adres IP jest przypisany do usługi w chmurze, która została wdrożona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="37c29-166">The reserved IP is assigned to the cloud service that the VM has been deployed to.</span></span> <span data-ttu-id="37c29-167">Jeśli chcesz się połączyć z maszyną wirtualną przez IP bezpośrednio, należy skonfigurować publicznego adresu IP poziomie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="37c29-167">If you want to connect to a VM by IP directly, you have to configure an instance-level public IP.</span></span> <span data-ttu-id="37c29-168">Publiczny adres IP poziomie wystąpienia jest typu publicznego adresu IP (nazywane ILPIP) przypisanej bezpośrednio do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="37c29-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM.</span></span> <span data-ttu-id="37c29-169">Nie można zarezerwować.</span><span class="sxs-lookup"><span data-stu-id="37c29-169">It cannot be reserved.</span></span> <span data-ttu-id="37c29-170">Aby uzyskać więcej informacji, przeczytaj [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="37c29-170">For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="37c29-171">Usuwanie zastrzeżonego adresu IP z wykonywanego wdrożenia</span><span class="sxs-lookup"><span data-stu-id="37c29-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="37c29-172">Aby usunąć zastrzeżonego adresu IP, dodać do nowej usługi w chmurze, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37c29-172">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="37c29-173">Usuwanie zastrzeżonego adresu IP z wykonywanego wdrożenia nie powoduje usunięcia zastrzeżenia z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="37c29-173">Removing a reserved IP from a running deployment does not remove the reservation from your subscription.</span></span> <span data-ttu-id="37c29-174">Po prostu powoduje zwolnienie IP ma być używany przez inny zasób w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="37c29-174">It simply frees the IP to be used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="37c29-175">Skojarzyć zastrzeżonego adresu IP do uruchomionego wdrożenia</span><span class="sxs-lookup"><span data-stu-id="37c29-175">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="37c29-176">Następujące polecenia tworzenia usługi w chmurze o nazwie *TestService2* z nowej maszyny Wirtualnej o nazwie *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="37c29-176">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="37c29-177">Istniejącego zastrzeżonego adresu IP o nazwie *MyReservedIP* jest następnie skojarzonego z usługą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="37c29-177">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="37c29-178">Skojarzyć zastrzeżonego adresu IP do usługi w chmurze przy użyciu pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="37c29-178">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="37c29-179">Można również skojarzyć zastrzeżonego adresu IP do usługi w chmurze przy użyciu pliku konfiguracji (CSCFG) usługi.</span><span class="sxs-lookup"><span data-stu-id="37c29-179">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="37c29-180">Następujące xml przykładowych pokazano, jak skonfigurować usługi w chmurze Użyj zastrzeżonego adresu VIP o nazwie *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="37c29-180">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="37c29-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="37c29-181">Next steps</span></span>
* <span data-ttu-id="37c29-182">Zrozumienie sposobu [adresowanie IP](virtual-network-ip-addresses-overview-classic.md) działa w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="37c29-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="37c29-183">Dowiedz się więcej o [prywatne adresy IP zarezerwowane](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="37c29-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="37c29-184">Dowiedz się więcej o [adresy IP publicznego poziom wystąpienia (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="37c29-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

