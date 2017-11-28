---
title: "aaaMutiple adresy VIP dla usługi w chmurze"
description: "Omówienie z wieloma wirtualnymi adresami IP i w jaki sposób tooset wielu adresów VIP na usługi w chmurze"
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
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="99c2f-103">Konfigurowanie wielu adresów VIP dla usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="99c2f-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="99c2f-104">Usługi w chmurze Azure dostępne za pośrednictwem hello podane publicznego Internetu przy użyciu adresu IP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="99c2f-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="99c2f-105">Ten publiczny adres IP jest określony tooas VIP (wirtualny adres IP), ponieważ jest on połączony toohello Azure Usługa równoważenia obciążenia, a nie hello wystąpień maszyn wirtualnych (VM) w ramach usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="99c2f-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="99c2f-106">Można uzyskać dostępu do dowolnego wystąpienia maszyny Wirtualnej w ramach usługi w chmurze przy użyciu pojedynczego wirtualnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="99c2f-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="99c2f-107">Istnieją jednak scenariuszy, w których może wymagać więcej niż jeden VIP jako toohello punktu wejścia sama usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="99c2f-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="99c2f-108">Na przykład usługi w chmurze może hostować wiele witryn sieci Web, które wymagają łączności SSL przy użyciu hello domyślnego portu 443, ponieważ każda lokacja jest hostowana dla różnych klientów lub dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="99c2f-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="99c2f-109">W tym scenariuszu należy toohave inny publiczny połączonej adres IP dla każdej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="99c2f-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="99c2f-110">Witaj Poniższy diagram przedstawia typowy wielodostępne hostingu sieci web potrzebujących SSL wielu certyfikatów na powitania sam port publiczny.</span><span class="sxs-lookup"><span data-stu-id="99c2f-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Scenariusz Multi VIP SSL](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="99c2f-112">W przykładzie hello powyżej, wszystkie wirtualne adresy IP Użyj hello ruchu i tym samym port publiczny (port 443) jest przekierowane tooone, lub więcej obciążenia zrównoważonym maszyn wirtualnych na unikatowy port prywatny hello wewnętrznego adresu IP usługi w chmurze hello hosting wszystkich hello witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="99c2f-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="99c2f-113">Inny hello Użyj hello wymagające sytuacji wieloma wirtualnymi adresami IP obsługuje wiele odbiorniki grupy dostępności funkcji SQL AlwaysOn na powitania sam zestaw maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="99c2f-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="99c2f-114">Wirtualne adresy IP są dynamiczne domyślnie, co oznacza, że hello rzeczywistego adresu IP przypisanego toohello usługi w chmurze mogą się zmieniać wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="99c2f-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="99c2f-115">tooprevent czy zapobiec, istnieje możliwość rezerwowania adresu VIP dla usługi.</span><span class="sxs-lookup"><span data-stu-id="99c2f-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="99c2f-116">toolearn więcej informacji na temat zarezerwowane wirtualne adresy IP, zobacz [zastrzeżone publicznego adresu IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="99c2f-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="99c2f-117">Zobacz [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses/) Aby uzyskać informacje o cenach na adresy VIP i zarezerwowane adresy IP.</span><span class="sxs-lookup"><span data-stu-id="99c2f-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="99c2f-118">Można używać środowiska PowerShell tooverify hello wirtualne adresy IP używane przez usług w chmurze, oraz dodawania i Usuń VIP, skojarzyć punkt końcowy tooan VIP oraz konfigurowanie równoważenia na określonego adresu VIP obciążenia.</span><span class="sxs-lookup"><span data-stu-id="99c2f-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="99c2f-119">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="99c2f-119">Limitations</span></span>

<span data-ttu-id="99c2f-120">W tej chwili funkcja wielu adresów VIP jest ograniczony toohello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="99c2f-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="99c2f-121">**Tylko IaaS**.</span><span class="sxs-lookup"><span data-stu-id="99c2f-121">**IaaS only**.</span></span> <span data-ttu-id="99c2f-122">Można włączyć tylko Multi VIP dla usług w chmurze, które zawierają maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="99c2f-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="99c2f-123">Nie można użyć adresu VIP wielu wystąpień roli PaaS scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="99c2f-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="99c2f-124">**PowerShell tylko**.</span><span class="sxs-lookup"><span data-stu-id="99c2f-124">**PowerShell only**.</span></span> <span data-ttu-id="99c2f-125">Wiele adresów VIP może zarządzać tylko przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99c2f-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="99c2f-126">Ograniczenia te są tymczasowe i mogą ulec zmianie w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="99c2f-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="99c2f-127">Upewnij się, że toorevisit tej strony tooverify przyszłe zmiany.</span><span class="sxs-lookup"><span data-stu-id="99c2f-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="99c2f-128">Jak usługa w chmurze tooa tooadd adresu VIP</span><span class="sxs-lookup"><span data-stu-id="99c2f-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="99c2f-129">Usługa tooyour tooadd adresu VIP, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="99c2f-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="99c2f-130">To polecenie wyświetla wynik toohello podobne, następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="99c2f-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="99c2f-131">Jak tooremove adresu VIP z usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="99c2f-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="99c2f-132">tooremove hello VIP dodawane tooyour usługi na przykład Witaj powyżej hello uruchom następujące polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="99c2f-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="99c2f-133">Można usunąć adresu VIP, jeśli ma ona nie tooit punkty końcowe skojarzone.</span><span class="sxs-lookup"><span data-stu-id="99c2f-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="99c2f-134">Jak tooretrieve VIP informacji z usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="99c2f-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="99c2f-135">tooretrieve hello wirtualne adresy IP skojarzone z usługą w chmurze, uruchom hello następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="99c2f-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="99c2f-136">skrypt Hello wyświetla wynik toohello podobne, następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="99c2f-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="99c2f-137">W tym przykładzie usługa w chmurze hello ma 3 wirtualne adresy IP:</span><span class="sxs-lookup"><span data-stu-id="99c2f-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="99c2f-138">**Adres Vip1** jest hello domyślny adres VIP, wiesz, że ponieważ hello IsDnsProgrammedName jest ustawiany tootrue.</span><span class="sxs-lookup"><span data-stu-id="99c2f-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="99c2f-139">**Vip2** i **Vip3** nie są używane jako nie mają adresy IP.</span><span class="sxs-lookup"><span data-stu-id="99c2f-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="99c2f-140">One tylko będzie używany, jeśli skojarzone toohello punktu końcowego adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="99c2f-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="99c2f-141">Subskrypcją będzie obciążana dla dodatkowe wirtualne adresy IP, gdy są one powiązane z punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="99c2f-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="99c2f-142">Aby uzyskać więcej informacji o cenach, zobacz [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="99c2f-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="99c2f-143">Jak punktu końcowego tooan tooassociate adresu VIP</span><span class="sxs-lookup"><span data-stu-id="99c2f-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="99c2f-144">tooassociate adresu VIP w chmurze tooan punkt końcowy usługi, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="99c2f-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="99c2f-145">Witaj polecenie tworzy punkt końcowy o nazwie adresów VIP połączonych toohello *Vip2* na porcie *80*i łączy go toohello maszyny Wirtualnej o nazwie *myVM1* w usłudze w chmurze o nazwie  *Moja_usługa* przy użyciu *TCP* na porcie *8080*.</span><span class="sxs-lookup"><span data-stu-id="99c2f-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="99c2f-146">tooverify hello konfiguracji, uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="99c2f-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="99c2f-147">Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="99c2f-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="99c2f-148">Jak tooenable Równoważenie obciążenia na określonych adresów VIP</span><span class="sxs-lookup"><span data-stu-id="99c2f-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="99c2f-149">Pojedynczego wirtualnego adresu IP można skojarzyć z wieloma maszynami wirtualnymi na potrzeby równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="99c2f-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="99c2f-150">Przykładowo, jeśli masz usługi w chmurze o nazwie *Moja_usługa*i dwie maszyny wirtualne o nazwie *myVM1* i *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="99c2f-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="99c2f-151">I usługi w chmurze ma wiele adresów VIP, jeden z nich o nazwie *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="99c2f-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="99c2f-152">Jeśli chcesz, aby cały ruch tooport tooensure *81* na *Vip2* jest rozmieszczana między *myVM1* i *myVM2* na porcie *8181* Uruchom hello następujący skrypt programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="99c2f-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="99c2f-153">Można także zaktualizować Twojego toouse usługi równoważenia obciążenia różnych adresów VIP.</span><span class="sxs-lookup"><span data-stu-id="99c2f-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="99c2f-154">Na przykład po uruchomieniu poniższego polecenia programu PowerShell hello ulegnie zmianie toouse zestaw o nazwie adresu Vip1 adresu VIP do równoważenia obciążenia hello:</span><span class="sxs-lookup"><span data-stu-id="99c2f-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="99c2f-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99c2f-155">Next Steps</span></span>

[<span data-ttu-id="99c2f-156">Analiza dzienników Azure Równoważenie obciążenia</span><span class="sxs-lookup"><span data-stu-id="99c2f-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="99c2f-157">Omówienie usługi równoważenia obciążenia połączonej Internet</span><span class="sxs-lookup"><span data-stu-id="99c2f-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="99c2f-158">Przed rozpoczęciem pracy internetowy modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="99c2f-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="99c2f-159">Omówienie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="99c2f-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="99c2f-160">Interfejsy API REST zastrzeżonego adresu IP</span><span class="sxs-lookup"><span data-stu-id="99c2f-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
