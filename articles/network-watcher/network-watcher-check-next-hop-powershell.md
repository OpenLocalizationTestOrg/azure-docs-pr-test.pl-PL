---
title: "Znajdź następny przeskok z Azure sieci obserwatora następnego przeskoku - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak znaleźć, co to jest typ następnego przeskoku i adres ip za pomocą następnego przeskoku przy użyciu programu PowerShell."
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
ms.openlocfilehash: 00161e7c6fb4becdb7d8eab266fa27128e50f8ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="42ad6-103">Sprawdź, jaki typ następnego przeskoku jest przy użyciu funkcji w następnym przeskoku w obserwatora sieciowego Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="42ad6-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="42ad6-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="42ad6-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="42ad6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="42ad6-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="42ad6-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="42ad6-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="42ad6-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="42ad6-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="42ad6-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="42ad6-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="42ad6-109">Następny przeskok jest funkcją obserwatora sieciowego, który zapewnia możliwość get Typ następnego przeskoku i adres IP na podstawie określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="42ad6-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="42ad6-110">Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne na uzyskanie dostępu do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="42ad6-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="42ad6-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="42ad6-111">Before you begin</span></span>

<span data-ttu-id="42ad6-112">W tym scenariuszu użyjesz portalu Azure można znaleźć Typ następnego przeskoku i adres IP.</span><span class="sxs-lookup"><span data-stu-id="42ad6-112">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="42ad6-113">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="42ad6-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="42ad6-114">Scenariusz również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje ma być używany.</span><span class="sxs-lookup"><span data-stu-id="42ad6-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="42ad6-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="42ad6-115">Scenario</span></span>

<span data-ttu-id="42ad6-116">Scenariusz omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku i adres IP dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="42ad6-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="42ad6-117">Aby dowiedzieć się więcej na temat następnego przeskoku, odwiedź stronę [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42ad6-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="42ad6-118">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="42ad6-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="42ad6-119">Pierwszym krokiem jest pobrać wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="42ad6-119">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="42ad6-120">`$networkWatcher` Zmienna jest przekazywana do następnego przeskoku Sprawdź polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42ad6-120">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="42ad6-121">Uzyskiwanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="42ad6-121">Get a virtual machine</span></span>

<span data-ttu-id="42ad6-122">Następny przeskok zwraca następnego przeskoku i adres IP następnego przeskoku z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="42ad6-122">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="42ad6-123">Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42ad6-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="42ad6-124">Jeśli znasz już identyfikator maszyny wirtualnej do użycia, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="42ad6-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="42ad6-125">Następnego przeskoku wymaga, aby zasobu maszyny Wirtualnej jest przydzielona do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="42ad6-125">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="get-the-network-interfaces"></a><span data-ttu-id="42ad6-126">Pobierz interfejsy sieciowe</span><span class="sxs-lookup"><span data-stu-id="42ad6-126">Get the network interfaces</span></span>

<span data-ttu-id="42ad6-127">Adres IP karty sieciowej na maszynie wirtualnej jest potrzebne w tym przykładzie Pobieramy kart sieciowych w maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="42ad6-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="42ad6-128">Jeśli znasz już adres IP, który ma zostać przetestowana na maszynie wirtualnej, można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="42ad6-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="42ad6-129">Pobierz następnego skoku</span><span class="sxs-lookup"><span data-stu-id="42ad6-129">Get Next Hop</span></span>

<span data-ttu-id="42ad6-130">Teraz nazywamy `Get-AzureRmNetworkWatcherNextHop` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42ad6-130">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="42ad6-131">Polecenie cmdlet jest przekazywana obserwatora sieciowego, maszynę wirtualną identyfikator źródłowy adres IP i docelowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="42ad6-131">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="42ad6-132">W tym przykładzie docelowy adres IP jest z maszyną wirtualną w innej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="42ad6-132">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="42ad6-133">Brak bramy sieci wirtualnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="42ad6-133">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="42ad6-134">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="42ad6-134">Review results</span></span>

<span data-ttu-id="42ad6-135">Po zakończeniu znajdują się wyniki.</span><span class="sxs-lookup"><span data-stu-id="42ad6-135">When complete, the results are provided.</span></span> <span data-ttu-id="42ad6-136">A także typ zasobu, który jest zwracany jest adres IP następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="42ad6-136">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="42ad6-137">W tym scenariuszu jest publiczny adres IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="42ad6-137">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="42ad6-138">Poniższa lista zawiera aktualnie dostępne wartości Typ następnego przeskoku:</span><span class="sxs-lookup"><span data-stu-id="42ad6-138">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="42ad6-139">**Typ następnego przeskoku**</span><span class="sxs-lookup"><span data-stu-id="42ad6-139">**Next Hop Type**</span></span>

* <span data-ttu-id="42ad6-140">Internet</span><span class="sxs-lookup"><span data-stu-id="42ad6-140">Internet</span></span>
* <span data-ttu-id="42ad6-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="42ad6-141">VirtualAppliance</span></span>
* <span data-ttu-id="42ad6-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="42ad6-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="42ad6-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="42ad6-143">VnetLocal</span></span>
* <span data-ttu-id="42ad6-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="42ad6-144">HyperNetGateway</span></span>
* <span data-ttu-id="42ad6-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="42ad6-145">VnetPeering</span></span>
* <span data-ttu-id="42ad6-146">Brak</span><span class="sxs-lookup"><span data-stu-id="42ad6-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="42ad6-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42ad6-147">Next steps</span></span>

<span data-ttu-id="42ad6-148">Dowiedz się, jak programowo Przejrzyj ustawienia sieciowe grupy zabezpieczeń, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="42ad6-148">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















