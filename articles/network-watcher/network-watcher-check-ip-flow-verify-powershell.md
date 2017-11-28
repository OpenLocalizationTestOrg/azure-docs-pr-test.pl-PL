---
title: "Sprawdź aaaverify ruchu z przepływem IP obserwatora sieci platformy Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub odrzucany, przy użyciu programu PowerShell"
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
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="90b7e-103">Sprawdź, czy ruch jest dozwolony lub odrzucany tooor z maszyny Wirtualnej z przepływem IP Sprawdź składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="90b7e-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="90b7e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="90b7e-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="90b7e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90b7e-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="90b7e-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="90b7e-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="90b7e-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="90b7e-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="90b7e-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="90b7e-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="90b7e-109">Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90b7e-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="90b7e-110">Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać tooan zasobu zewnętrznego i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90b7e-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="90b7e-111">Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="90b7e-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="90b7e-112">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.</span><span class="sxs-lookup"><span data-stu-id="90b7e-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="90b7e-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="90b7e-113">Before you begin</span></span>

<span data-ttu-id="90b7e-114">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego lub istniejącego wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="90b7e-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="90b7e-115">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="90b7e-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="90b7e-116">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="90b7e-116">Scenario</span></span>

<span data-ttu-id="90b7e-117">Ten scenariusz używa IP przepływ Sprawdź tooverify maszynę wirtualną można, rozmawiać tooa będzie znane adresu IP usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="90b7e-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="90b7e-118">Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="90b7e-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="90b7e-119">więcej informacji na temat przepływu IP sprawdzić, odwiedź stronę toolearn [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="90b7e-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="90b7e-120">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="90b7e-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="90b7e-121">pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="90b7e-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="90b7e-122">Witaj `$networkWatcher` zmienna jest przekazywana toohello IP przepływu Sprawdź polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="90b7e-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="90b7e-123">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="90b7e-123">Get a VM</span></span>

<span data-ttu-id="90b7e-124">Przepływ IP Sprawdź testy tooor ruch z adresu IP na tooor maszyny wirtualnej, z zdalnego miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="90b7e-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="90b7e-125">Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="90b7e-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="90b7e-126">Jeśli znasz już identyfikator hello hello toouse maszyny wirtualnej, można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="90b7e-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="90b7e-127">Pobierz hello kart Sieciowych</span><span class="sxs-lookup"><span data-stu-id="90b7e-127">Get hello NICS</span></span>

<span data-ttu-id="90b7e-128">adres IP karty Sieciowej na maszynie wirtualnej hello Hello jest potrzebne w tym przykładzie Pobieramy hello karty interfejsu sieciowego na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90b7e-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="90b7e-129">Jeśli znasz już IP hello adresu, który ma tootest na maszynie wirtualnej hello, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="90b7e-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="90b7e-130">Sprawdź uruchomienia przepływu IP</span><span class="sxs-lookup"><span data-stu-id="90b7e-130">Run IP flow verify</span></span>

<span data-ttu-id="90b7e-131">Teraz, gdy mamy informacji hello potrzebne toorun hello polecenia cmdlet, przeprowadzana hello `Test-AzureRmNetworkWatcherIPFlow` ruchu hello tootest polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="90b7e-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="90b7e-132">W tym przykładzie używamy hello pierwszego adresu IP na powitania pierwszej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="90b7e-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="90b7e-133">Sprawdź przepływ IP wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.</span><span class="sxs-lookup"><span data-stu-id="90b7e-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="90b7e-134">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="90b7e-134">Review Results</span></span>

<span data-ttu-id="90b7e-135">Po uruchomieniu `Test-AzureRmNetworkWatcherIPFlow` hello wyniki są zwracane, hello poniższym przykładzie jest hello wyniki zwrócone z hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="90b7e-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="90b7e-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90b7e-136">Next steps</span></span>

<span data-ttu-id="90b7e-137">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które są zdefiniowane w dół.</span><span class="sxs-lookup"><span data-stu-id="90b7e-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













