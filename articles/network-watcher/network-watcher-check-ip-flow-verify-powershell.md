---
title: "Sprawdź ruchu z adresem IP obserwatora sieci Azure przepływ weryfikacji - programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób sprawdzania, jeśli ruch do i z maszyny wirtualnej jest dozwolona lub odmowa przy użyciu programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: bf0c01a9af0e28647d11ad89a9d164716d5c8312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="c0016-103">Sprawdź, czy ruch jest dozwolony lub odrzucany do lub z maszyny Wirtualnej z przepływem IP Sprawdź składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="c0016-103">Check if traffic is allowed or denied to or from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c0016-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c0016-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="c0016-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0016-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="c0016-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="c0016-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="c0016-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="c0016-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="c0016-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="c0016-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="c0016-109">Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który pozwala sprawdzić, jeśli ruch jest dozwolony na lub z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c0016-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="c0016-110">Ten scenariusz przydaje się pobrać bieżący stan tego, czy maszyny wirtualne mogą komunikować się z zasobu zewnętrznego i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c0016-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="c0016-111">Sprawdź przepływ IP pozwala sprawdzić, czy reguł sieciowej grupy zabezpieczeń (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="c0016-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="c0016-112">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź jest zapewnienie ruchu, który ma być zablokowana jest prawidłowo blokowane przez grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="c0016-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0016-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c0016-113">Before you begin</span></span>

<span data-ttu-id="c0016-114">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) do tworzenia obserwatora sieciowego lub mieć istniejące wystąpienie obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c0016-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="c0016-115">Scenariusz również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje ma być używany.</span><span class="sxs-lookup"><span data-stu-id="c0016-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="c0016-116">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="c0016-116">Scenario</span></span>

<span data-ttu-id="c0016-117">Ten scenariusz używa IP przepływ Sprawdź, aby sprawdzić, czy maszyna wirtualna może komunikować się znanego adresu IP usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="c0016-117">This scenario uses IP flow verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="c0016-118">Jeśli ruch jest niedozwolone, zwraca zasady zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="c0016-118">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="c0016-119">Aby dowiedzieć się więcej na temat przepływu IP sprawdzić, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c0016-119">To learn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="c0016-120">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="c0016-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="c0016-121">Pierwszym krokiem jest pobrać wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c0016-121">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="c0016-122">`$networkWatcher` Zmienna jest przekazywana do adresu IP przepływu Sprawdź polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c0016-122">The `$networkWatcher` variable is passed to the IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="c0016-123">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c0016-123">Get a VM</span></span>

<span data-ttu-id="c0016-124">Przepływ IP Sprawdź testy ruchu do lub z adresu IP na maszynie wirtualnej lub zdalnego miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="c0016-124">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="c0016-125">Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c0016-125">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="c0016-126">Jeśli znasz już identyfikator maszyny wirtualnej do użycia, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="c0016-126">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-the-nics"></a><span data-ttu-id="c0016-127">Pobierz karty interfejsu Sieciowego</span><span class="sxs-lookup"><span data-stu-id="c0016-127">Get the NICS</span></span>

<span data-ttu-id="c0016-128">Adres IP karty sieciowej na maszynie wirtualnej jest potrzebne w tym przykładzie Pobieramy kart sieciowych w maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c0016-128">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="c0016-129">Jeśli znasz już adres IP, który ma zostać przetestowana na maszynie wirtualnej, można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="c0016-129">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="c0016-130">Sprawdź uruchomienia przepływu IP</span><span class="sxs-lookup"><span data-stu-id="c0016-130">Run IP flow verify</span></span>

<span data-ttu-id="c0016-131">Teraz, gdy mamy informacje potrzebne do uruchomienia polecenia cmdlet, możemy uruchomić `Test-AzureRmNetworkWatcherIPFlow` polecenia cmdlet, aby przetestować ruchu.</span><span class="sxs-lookup"><span data-stu-id="c0016-131">Now that we have the information needed to run the cmdlet, we run the `Test-AzureRmNetworkWatcherIPFlow` cmdlet to test the traffic.</span></span> <span data-ttu-id="c0016-132">W tym przykładzie użyto pierwszego adresu IP na pierwszej karcie sieciowej.</span><span class="sxs-lookup"><span data-stu-id="c0016-132">In this example, we are using the first IP address on the first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="c0016-133">Sprawdź przepływ IP wymaga, aby zasobu maszyny Wirtualnej jest przydzielona do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="c0016-133">IP flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="c0016-134">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="c0016-134">Review Results</span></span>

<span data-ttu-id="c0016-135">Po uruchomieniu `Test-AzureRmNetworkWatcherIPFlow` wyniki są zwracane, w poniższym przykładzie jest wyników zwróconych z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="c0016-135">After running `Test-AzureRmNetworkWatcherIPFlow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="c0016-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c0016-136">Next steps</span></span>

<span data-ttu-id="c0016-137">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) śledzić reguły zabezpieczeń sieciowych grupy i zabezpieczeń zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="c0016-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













