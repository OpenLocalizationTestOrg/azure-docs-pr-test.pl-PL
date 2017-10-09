---
title: "aaaCreate wewnętrznego Azure PowerShell klasycznego moduł równoważenia - obciążenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w hello klasycznego modelu wdrażania przy użyciu programu PowerShell obciążenia toocreate jako wewnętrzne"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="5d157-103">Wprowadzenie do tworzenia wewnętrznego modułu równoważenia obciążenia (klasycznego) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d157-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d157-104">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d157-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="5d157-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5d157-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="5d157-106">Usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="5d157-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="5d157-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5d157-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="5d157-108">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="5d157-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="5d157-109">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5d157-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5d157-110">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5d157-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="5d157-111">Tworzenie zestawu wewnętrznego modułu równoważenia obciążenia dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="5d157-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="5d157-112">toocreate wewnętrznego modułu równoważenia obciążenia ustaw i hello serwerów, które będzie wysyłać ich tooit ruchu sieciowego, masz następujące hello toodo:</span><span class="sxs-lookup"><span data-stu-id="5d157-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="5d157-113">Utwórz wystąpienie wewnętrzne Równoważenie obciążenia sieciowego, który będzie hello punkt końcowy przychodzącego ruchu toobe równoważone między serwerami hello zestawu z równoważeniem obciążenia.</span><span class="sxs-lookup"><span data-stu-id="5d157-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="5d157-114">Dodawanie punktów końcowych odpowiadającego toohello maszyn wirtualnych, które będzie otrzymywał hello ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="5d157-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="5d157-115">Konfigurowanie serwerów hello, które będą wysyłane się, że hello ruchu toobe o zrównoważonym obciążeniu toosend ich ruchu toohello wirtualny adres IP (VIP) wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5d157-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="5d157-116">Krok 1: utwórz wystąpienie wewnętrznego równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="5d157-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="5d157-117">Dla istniejącej usługi w chmurze lub wdrożyć w obszarze regionalnej sieci wirtualnej usługi w chmurze można utworzyć wystąpienia wewnętrzne Równoważenie obciążenia sieciowego z hello następujących poleceń programu Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5d157-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="5d157-118">Należy pamiętać, że to zastosowanie hello [AzureEndpoint Dodaj](https://msdn.microsoft.com/library/dn495300.aspx) zestaw parametrów DefaultProbe hello używa polecenia cmdlet programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d157-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="5d157-119">Aby uzyskać więcej informacji na temat dodatkowych zestawów parametrów, zobacz artykuł [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d157-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="5d157-120">Krok 2: Dodawanie punktów końcowych toohello równoważenia obciążenia wewnętrznego wystąpienia</span><span class="sxs-lookup"><span data-stu-id="5d157-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="5d157-121">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="5d157-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="5d157-122">Krok 3: Konfigurowanie Twojego toosend serwerów ich ruchu toohello nowego wewnętrzne Równoważenie obciążenia sieciowego punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="5d157-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="5d157-123">Ma zbyt skonfigurować serwery hello, których ruch jest będzie toobe ze zrównoważonym obciążeniem toouse hello nowy adres IP (hello VIP) hello wystąpienia wewnętrzne Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5d157-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="5d157-124">Jest to adres hello, na które hello równoważenia obciążenia wewnętrznego nasłuchuje wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="5d157-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="5d157-125">W większości przypadków należy toojust dodawania lub modyfikowania rekordu DNS dla hello VIP wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5d157-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="5d157-126">Jeśli określony adres IP hello podczas tworzenia hello wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego, masz już hello VIP.</span><span class="sxs-lookup"><span data-stu-id="5d157-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="5d157-127">W przeciwnym razie można wyświetlić VIP hello z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5d157-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="5d157-128">toouse tych poleceń, wprowadź wartości hello i Usuń hello < i >.</span><span class="sxs-lookup"><span data-stu-id="5d157-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="5d157-129">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="5d157-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="5d157-130">Z widoku hello hello polecenia Get-AzureInternalLoadBalancer Zanotuj adres IP hello i serwery tooyour niezbędne zmiany hello lub tooensure rekordy DNS, który toohello VIP pobiera skierować ruchu związanego z.</span><span class="sxs-lookup"><span data-stu-id="5d157-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="5d157-131">platformy Microsoft Azure Hello używa statycznych, publicznie routingu adresów IPv4 dla różnych scenariuszy administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="5d157-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="5d157-132">adres IP Hello jest 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="5d157-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="5d157-133">Ten adres IP nie powinien być blokowany przez zapory, ponieważ może to spowodować nieoczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="5d157-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="5d157-134">Z zakresie tooAzure wewnętrzne Równoważenie obciążenia sieciowego ten adres IP jest używana przez monitorowanie sond z stan kondycji hello toodetermine usługi równoważenia obciążenia powitania dla maszyn wirtualnych w zestawie o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="5d157-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="5d157-135">Jeśli grupa zabezpieczeń sieci jest toorestrict używanych maszyn wirtualnych tooAzure ruchu w zestawie wewnętrznie równoważeniem obciążenia lub zastosowane tooa podsieci sieci wirtualnej, upewnij się, że reguły zabezpieczeń sieci został dodany ruchu tooallow 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="5d157-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="5d157-136">Przykład wewnętrznego równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="5d157-136">Example of internal load balancing</span></span>

<span data-ttu-id="5d157-137">toostep hello zakończenia tooend proces tworzenia zestawu z równoważeniem obciążenia dla dwóch przykładowe konfiguracje, zobaczysz hello w następujących sekcjach.</span><span class="sxs-lookup"><span data-stu-id="5d157-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="5d157-138">Aplikacja wielowarstwowa, dostępna z Internetu</span><span class="sxs-lookup"><span data-stu-id="5d157-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="5d157-139">Ma tooprovide usługi równoważenia obciążenia bazy danych dla zestawu serwerów sieci web skierowane do Internetu.</span><span class="sxs-lookup"><span data-stu-id="5d157-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="5d157-140">Oba zestawy serwerów są hostowane na jednej usłudze w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="5d157-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="5d157-141">Port 1433 tooTCP ruchu serwera sieci Web muszą być dystrybuowane między dwiema maszynami wirtualnymi w hello warstwy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5d157-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="5d157-142">Rysunek 1 pokazuje konfigurację hello.</span><span class="sxs-lookup"><span data-stu-id="5d157-142">Figure 1 shows hello configuration.</span></span>

![Wewnętrzny zestawu z równoważeniem obciążenia dla warstwy bazy danych hello](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="5d157-144">Konfiguracja Hello obejmuje następujące hello:</span><span class="sxs-lookup"><span data-stu-id="5d157-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="5d157-145">Witaj istniejącą usługę w chmurze hostowania maszyn wirtualnych hello nosi nazwę mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="5d157-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="5d157-146">dwa istniejących serwerów bazy danych Hello są nazywane DB1, bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="5d157-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="5d157-147">Serwery sieci Web w warstwie web hello połączenia toohello serwerów baz danych w warstwie bazy danych hello przy użyciu hello prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5d157-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="5d157-148">Inną opcją jest toouse własnego systemu DNS dla sieci wirtualnej hello i ręcznie zarejestrować rekordu A dla zestawu modułu równoważenia obciążenia wewnętrznego hello.</span><span class="sxs-lookup"><span data-stu-id="5d157-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="5d157-149">Witaj następujące polecenia Skonfiguruj nowe wystąpienie wewnętrzny równoważenia obciążenia o nazwie **ILBset** i Dodaj maszyny wirtualne toohello punkty końcowe odpowiadającego toohello dwa serwery baz danych:</span><span class="sxs-lookup"><span data-stu-id="5d157-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="5d157-150">Usuwanie konfiguracji wewnętrznego równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="5d157-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="5d157-151">tooremove maszynę wirtualną jako punkt końcowy z wystąpieniem usługi równoważenia obciążenia wewnętrznego hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5d157-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="5d157-152">toouse tych poleceń, podaj wartości hello, usuwanie hello < i >.</span><span class="sxs-lookup"><span data-stu-id="5d157-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="5d157-153">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="5d157-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="5d157-154">tooremove wystąpienia usługi równoważenia obciążenia wewnętrznego z usługą w chmurze, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5d157-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="5d157-155">toouse tych poleceń, wypełnij wartość hello i Usuń hello < i >.</span><span class="sxs-lookup"><span data-stu-id="5d157-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="5d157-156">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="5d157-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="5d157-157">Dodatkowe informacje na temat poleceń cmdlet wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="5d157-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="5d157-158">tooobtain dodatkowe informacje dotyczące równoważenia obciążenia wewnętrznego poleceń cmdlet narzędzia, uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="5d157-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="5d157-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d157-159">Next steps</span></span>

<span data-ttu-id="5d157-160">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)</span><span class="sxs-lookup"><span data-stu-id="5d157-160">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="5d157-161">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="5d157-161">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>

