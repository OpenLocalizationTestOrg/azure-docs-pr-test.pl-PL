---
title: "Wiele adresów VIP dla usługi w chmurze"
description: "Omówienie wieloma wirtualnymi adresami IP oraz jak ustawić wiele adresów VIP na usługi w chmurze"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="6ace1-103">Konfigurowanie wielu adresów VIP dla usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="6ace1-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="6ace1-104">Usługi w chmurze Azure mogą korzystać za pośrednictwem publicznej sieci Internet, za pomocą adresu IP podał Azure.</span><span class="sxs-lookup"><span data-stu-id="6ace1-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="6ace1-105">Ten publiczny adres IP jest określany jako VIP (wirtualny adres IP), ponieważ jest połączony z usługą równoważenia obciążenia Azure, a nie maszyna wirtualna (VM) wystąpień w ramach usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6ace1-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="6ace1-106">Można uzyskać dostępu do dowolnego wystąpienia maszyny Wirtualnej w ramach usługi w chmurze przy użyciu pojedynczego wirtualnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6ace1-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="6ace1-107">Istnieją jednak scenariuszy, w których może wymagać więcej niż jeden punkt VIP jako wpis do tej samej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6ace1-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="6ace1-108">Na przykład usługi w chmurze może hostować wiele witryn sieci Web, które wymagają łączności SSL przy użyciu domyślnego portu 443, ponieważ każda lokacja jest hostowana dla różnych klientów lub dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="6ace1-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="6ace1-109">W tym scenariuszu musisz mieć inny publiczny połączonej adres IP dla każdej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6ace1-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="6ace1-110">Na poniższym diagramie przedstawiono typowe wielodostępne hostingu potrzebuje wiele certyfikatów SSL na ten sam port publiczny.</span><span class="sxs-lookup"><span data-stu-id="6ace1-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Scenariusz Multi VIP SSL](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="6ace1-112">W powyższym przykładzie wszystkie wirtualne adresy IP Użyj tego samego portu publicznego (port 443), a ruch jest przekierowywany do jednej lub maszyn wirtualnych na unikatowy port prywatny dla wewnętrznego adresu IP usługi w chmurze hosting wszystkich witryn sieci Web o zrównoważonym obciążeniu więcej.</span><span class="sxs-lookup"><span data-stu-id="6ace1-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="6ace1-113">Innej sytuacji wymagających wielu adresy VIP obsługuje wiele odbiorniki grupy dostępności funkcji SQL AlwaysOn na ten sam zestaw maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6ace1-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="6ace1-114">Wirtualne adresy IP są dynamiczne domyślnie, co oznacza, że rzeczywista adresu IP przypisanego do usługi w chmurze mogą się zmieniać wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="6ace1-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="6ace1-115">Aby zapobiec który, może zarezerwować adresu VIP dla usługi.</span><span class="sxs-lookup"><span data-stu-id="6ace1-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="6ace1-116">Aby dowiedzieć się więcej na temat zarezerwowane wirtualne adresy IP, zobacz [zastrzeżone publicznego adresu IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="6ace1-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6ace1-117">Zobacz [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses/) Aby uzyskać informacje o cenach na adresy VIP i zarezerwowane adresy IP.</span><span class="sxs-lookup"><span data-stu-id="6ace1-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="6ace1-118">Można Sprawdź wirtualne adresy IP używane przez usługi chmury, za pomocą programu PowerShell, a także dodać i usunąć adresy VIP, skojarzyć VIP do punktu końcowego i konfigurowanie równoważenia na określonego adresu VIP obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6ace1-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="6ace1-119">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="6ace1-119">Limitations</span></span>

<span data-ttu-id="6ace1-120">W tej chwili funkcje wielu adresów VIP są ograniczone do następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="6ace1-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="6ace1-121">**Tylko IaaS**.</span><span class="sxs-lookup"><span data-stu-id="6ace1-121">**IaaS only**.</span></span> <span data-ttu-id="6ace1-122">Można włączyć tylko Multi VIP dla usług w chmurze, które zawierają maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="6ace1-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="6ace1-123">Nie można użyć adresu VIP wielu wystąpień roli PaaS scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="6ace1-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="6ace1-124">**PowerShell tylko**.</span><span class="sxs-lookup"><span data-stu-id="6ace1-124">**PowerShell only**.</span></span> <span data-ttu-id="6ace1-125">Wiele adresów VIP może zarządzać tylko przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6ace1-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="6ace1-126">Ograniczenia te są tymczasowe i mogą ulec zmianie w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="6ace1-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="6ace1-127">Upewnij się, że ponownie tę stronę, aby sprawdzić przyszłe zmiany.</span><span class="sxs-lookup"><span data-stu-id="6ace1-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="6ace1-128">Jak dodać adresu VIP usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="6ace1-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="6ace1-129">Aby dodać adresu VIP do usługi, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ace1-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="6ace1-130">To polecenie wyświetla wynik jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="6ace1-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="6ace1-131">Jak usunąć wirtualnego adresu IP z usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="6ace1-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="6ace1-132">Aby usunąć adres VIP dodane do usługi w powyższym przykładzie, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ace1-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="6ace1-133">Można usunąć adresu VIP, jeśli go nie ma punktów końcowych skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="6ace1-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="6ace1-134">Jak pobrać VIP informacji z usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="6ace1-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="6ace1-135">Aby pobrać wirtualne adresy IP skojarzone z usługą w chmurze, uruchom następujący skrypt programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ace1-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="6ace1-136">Skrypt zawiera wynik jest podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="6ace1-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="6ace1-137">W tym przykładzie usługa w chmurze ma 3 wirtualne adresy IP:</span><span class="sxs-lookup"><span data-stu-id="6ace1-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="6ace1-138">**Adres Vip1** jest domyślny adres VIP, wiesz, że ponieważ IsDnsProgrammedName jest ustawiany na wartość true.</span><span class="sxs-lookup"><span data-stu-id="6ace1-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="6ace1-139">**Vip2** i **Vip3** nie są używane jako nie mają adresy IP.</span><span class="sxs-lookup"><span data-stu-id="6ace1-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="6ace1-140">One będzie można używać tylko jeśli skojarzyć punkt końcowy do adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="6ace1-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="6ace1-141">Subskrypcją będzie obciążana dla dodatkowe wirtualne adresy IP, gdy są one powiązane z punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="6ace1-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="6ace1-142">Aby uzyskać więcej informacji o cenach, zobacz [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="6ace1-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="6ace1-143">Jak skojarzyć VIP do punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="6ace1-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="6ace1-144">Aby skojarzyć adresów VIP na punkt końcowy usługi w chmurze, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ace1-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="6ace1-145">Polecenie tworzy punkt końcowy powiązany adres VIP o nazwie *Vip2* na porcie *80*i łączy go z maszyny Wirtualnej o nazwie *myVM1* w usłudze w chmurze o nazwie *Moja_usługa* przy użyciu *TCP* na porcie *8080*.</span><span class="sxs-lookup"><span data-stu-id="6ace1-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="6ace1-146">Aby sprawdzić konfigurację, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ace1-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="6ace1-147">Dane wyjściowe wygląda podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="6ace1-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="6ace1-148">Jak włączyć równoważenia na określonego adresu VIP obciążenia</span><span class="sxs-lookup"><span data-stu-id="6ace1-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="6ace1-149">Pojedynczego wirtualnego adresu IP można skojarzyć z wieloma maszynami wirtualnymi na potrzeby równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6ace1-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="6ace1-150">Przykładowo, jeśli masz usługi w chmurze o nazwie *Moja_usługa*i dwie maszyny wirtualne o nazwie *myVM1* i *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="6ace1-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="6ace1-151">I usługi w chmurze ma wiele adresów VIP, jeden z nich o nazwie *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="6ace1-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="6ace1-152">Jeśli chcesz upewnić się, że cały ruch do portu *81* na *Vip2* jest rozmieszczana między *myVM1* i *myVM2* na porcie *8181* , uruchom następujący skrypt programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ace1-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="6ace1-153">Należy również zaktualizować przez moduł równoważenia obciążenia, aby użyć innego adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="6ace1-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="6ace1-154">Na przykład po uruchomieniu poniższego polecenia programu PowerShell ulegnie zmianie zestawu do używania adresu VIP o nazwie adresu Vip1 równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="6ace1-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="6ace1-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ace1-155">Next Steps</span></span>

[<span data-ttu-id="6ace1-156">Analiza dzienników Azure Równoważenie obciążenia</span><span class="sxs-lookup"><span data-stu-id="6ace1-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="6ace1-157">Omówienie usługi równoważenia obciążenia połączonej Internet</span><span class="sxs-lookup"><span data-stu-id="6ace1-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="6ace1-158">Przed rozpoczęciem pracy internetowy modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="6ace1-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6ace1-159">Omówienie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6ace1-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="6ace1-160">Interfejsy API REST zastrzeżonego adresu IP</span><span class="sxs-lookup"><span data-stu-id="6ace1-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
