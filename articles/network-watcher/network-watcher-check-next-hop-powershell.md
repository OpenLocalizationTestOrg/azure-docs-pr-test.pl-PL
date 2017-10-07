---
title: "aaaFind następnego przeskoku z Azure sieci obserwatora następnego przeskoku - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest przy użyciu adresu ip następnego przeskoku przy użyciu programu PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="ab643-103">Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab643-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ab643-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ab643-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="ab643-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab643-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="ab643-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="ab643-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="ab643-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="ab643-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="ab643-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="ab643-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="ab643-109">Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab643-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="ab643-110">Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.</span><span class="sxs-lookup"><span data-stu-id="ab643-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ab643-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ab643-111">Before you begin</span></span>

<span data-ttu-id="ab643-112">W tym scenariuszu użyje hello Typ następnego przeskoku hello toofind portalu Azure i adres IP.</span><span class="sxs-lookup"><span data-stu-id="ab643-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="ab643-113">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="ab643-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="ab643-114">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="ab643-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="ab643-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="ab643-115">Scenario</span></span>

<span data-ttu-id="ab643-116">Scenariusz Hello omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku hello i adres IP dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="ab643-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="ab643-117">odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab643-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="ab643-118">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="ab643-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="ab643-119">pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="ab643-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="ab643-120">Witaj `$networkWatcher` zmienna jest przekazywana toohello następnego przeskoku Sprawdź polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ab643-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="ab643-121">Uzyskiwanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab643-121">Get a virtual machine</span></span>

<span data-ttu-id="ab643-122">Następny przeskok zwraca hello następnego przeskoku i adres IP następnego przeskoku hello hello z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab643-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="ab643-123">Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="ab643-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="ab643-124">Jeśli znasz już identyfikator hello hello toouse maszyny wirtualnej, można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="ab643-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="ab643-125">Następnego przeskoku wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.</span><span class="sxs-lookup"><span data-stu-id="ab643-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="ab643-126">Pobierz interfejsy sieciowe hello</span><span class="sxs-lookup"><span data-stu-id="ab643-126">Get hello network interfaces</span></span>

<span data-ttu-id="ab643-127">adres IP karty Sieciowej na maszynie wirtualnej hello Hello jest potrzebne w tym przykładzie Pobieramy hello karty interfejsu sieciowego na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab643-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="ab643-128">Jeśli znasz już IP hello adresu, który ma tootest na maszynie wirtualnej hello, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="ab643-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="ab643-129">Pobierz następnego skoku</span><span class="sxs-lookup"><span data-stu-id="ab643-129">Get Next Hop</span></span>

<span data-ttu-id="ab643-130">Teraz nazywamy hello `Get-AzureRmNetworkWatcherNextHop` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ab643-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="ab643-131">Możemy przekazać hello polecenia cmdlet hello obserwatora sieciowego maszyny wirtualnej identyfikator, źródłowy adres IP i docelowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="ab643-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="ab643-132">W tym przykładzie hello docelowy adres IP jest tooa maszyny Wirtualnej w innej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab643-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="ab643-133">Między dwiema sieciami wirtualnymi hello jest bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab643-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="ab643-134">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="ab643-134">Review results</span></span>

<span data-ttu-id="ab643-135">Po zakończeniu hello wyniki są dostarczane.</span><span class="sxs-lookup"><span data-stu-id="ab643-135">When complete, hello results are provided.</span></span> <span data-ttu-id="ab643-136">oraz hello typ zasobu, który jest zwracany jest adres IP następnego przeskoku Hello.</span><span class="sxs-lookup"><span data-stu-id="ab643-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="ab643-137">W tym scenariuszu jest hello publicznego adresu IP bramy sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="ab643-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="ab643-138">Witaj Poniższa lista zawiera aktualnie dostępne wartości Typ następnego przeskoku hello:</span><span class="sxs-lookup"><span data-stu-id="ab643-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="ab643-139">**Typ następnego przeskoku**</span><span class="sxs-lookup"><span data-stu-id="ab643-139">**Next Hop Type**</span></span>

* <span data-ttu-id="ab643-140">Internet</span><span class="sxs-lookup"><span data-stu-id="ab643-140">Internet</span></span>
* <span data-ttu-id="ab643-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="ab643-141">VirtualAppliance</span></span>
* <span data-ttu-id="ab643-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="ab643-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="ab643-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="ab643-143">VnetLocal</span></span>
* <span data-ttu-id="ab643-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="ab643-144">HyperNetGateway</span></span>
* <span data-ttu-id="ab643-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="ab643-145">VnetPeering</span></span>
* <span data-ttu-id="ab643-146">Brak</span><span class="sxs-lookup"><span data-stu-id="ab643-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab643-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab643-147">Next steps</span></span>

<span data-ttu-id="ab643-148">Dowiedz się, jak tooreview ustawieniami grupy zabezpieczeń sieci programowo, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="ab643-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















