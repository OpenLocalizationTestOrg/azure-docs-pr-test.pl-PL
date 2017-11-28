---
title: "Sprawdź ruchu z przepływem IP obserwatora sieci platformy Azure Sprawdź — REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób sprawdzania, jeśli ruch do i z maszyny wirtualnej jest dozwolona lub odmowa"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="c1eb2-103">Sprawdź, czy ruch jest dozwolony lub odrzucany z przepływem IP Sprawdź składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="c1eb2-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c1eb2-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c1eb2-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="c1eb2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1eb2-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="c1eb2-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="c1eb2-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="c1eb2-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="c1eb2-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="c1eb2-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="c1eb2-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="c1eb2-109">Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który pozwala sprawdzić, jeśli ruch jest dozwolony na lub z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="c1eb2-110">Sprawdzanie poprawności może zostać uruchomione dla ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="c1eb2-111">Ten scenariusz przydaje się pobrać bieżący stan tego, czy maszyny wirtualne mogą komunikować się z zasobu zewnętrznego i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="c1eb2-112">Sprawdź przepływ IP pozwala sprawdzić, czy reguł sieciowej grupy zabezpieczeń (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="c1eb2-113">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź jest zapewnienie ruchu, który ma być zablokowana jest prawidłowo blokowane przez grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c1eb2-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c1eb2-114">Before you begin</span></span>

<span data-ttu-id="c1eb2-115">ARMclient służy do wywołania interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="c1eb2-116">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="c1eb2-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="c1eb2-117">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="c1eb2-118">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="c1eb2-118">Scenario</span></span>

<span data-ttu-id="c1eb2-119">W tym scenariuszu przepływu IP Sprawdź, czy można zweryfikować, jeśli maszyny wirtualnej mogą komunikować się z innego komputera za pośrednictwem portu 443.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="c1eb2-120">Jeśli ruch jest niedozwolone, zwraca zasady zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="c1eb2-121">Aby dowiedzieć się więcej o przepływie IP upewnij się, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c1eb2-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="c1eb2-122">W tym scenariuszu należy:</span><span class="sxs-lookup"><span data-stu-id="c1eb2-122">In this scenario, you:</span></span>

* <span data-ttu-id="c1eb2-123">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c1eb2-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="c1eb2-124">Sprawdź połączenie IP przepływu</span><span class="sxs-lookup"><span data-stu-id="c1eb2-124">Call IP flow verify</span></span>
* <span data-ttu-id="c1eb2-125">Sprawdź wyniki</span><span class="sxs-lookup"><span data-stu-id="c1eb2-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="c1eb2-126">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="c1eb2-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="c1eb2-127">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c1eb2-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="c1eb2-128">Uruchom następujący skrypt, aby wrócić do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="c1eb2-129">Poniższy kod wymaga wartości zmiennych:</span><span class="sxs-lookup"><span data-stu-id="c1eb2-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="c1eb2-130">**Identyfikator subskrypcji** — identyfikator do użycia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="c1eb2-131">**resourceGroupName** — Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="c1eb2-132">Informacje potrzebne jest identyfikatorem, w obszarze typu `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="c1eb2-133">Wyniki powinny być podobne do poniższego przykładu kodu:</span><span class="sxs-lookup"><span data-stu-id="c1eb2-133">The results should be similar to the following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="c1eb2-134">Wywołanie IP przepływu Sprawdź</span><span class="sxs-lookup"><span data-stu-id="c1eb2-134">Call IP flow Verify</span></span>

<span data-ttu-id="c1eb2-135">Poniższy przykład tworzy żądanie, aby zweryfikować ruchu dla określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="c1eb2-136">Odpowiedź zwraca, jeśli ruch jest dozwolony lub jeśli ruch jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="c1eb2-137">Jeśli ruch odmówiono ona również zwraca jakie reguła blokuje ruch.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="c1eb2-138">Sprawdź przepływ IP wymaga, aby zasobu maszyny Wirtualnej jest przydzielona.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="c1eb2-139">Ten skrypt wymaga zasobów identyfikator maszyny wirtualnej i karty interfejsu sieciowego na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="c1eb2-140">Wartości te są dostarczane przez poprzednie dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="c1eb2-141">Dla wszystkich wywołań REST obserwatora sieciowego Nazwa grupy zasobów w identyfikatorze URI żądania jest ten, który zawiera wystąpienie obserwatora sieciowego, nie zasoby, które są wykonywane czynności diagnostyczne, na.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-the-results"></a><span data-ttu-id="c1eb2-142">Opis wyników</span><span class="sxs-lookup"><span data-stu-id="c1eb2-142">Understanding the results</span></span>

<span data-ttu-id="c1eb2-143">Odpowiedź, wracając informuje, czy ruch jest dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="c1eb2-144">Odpowiedź wygląda jedną z poniższych przykładach:</span><span class="sxs-lookup"><span data-stu-id="c1eb2-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="c1eb2-145">**Dozwolone**</span><span class="sxs-lookup"><span data-stu-id="c1eb2-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="c1eb2-146">**Odmowa dostępu**</span><span class="sxs-lookup"><span data-stu-id="c1eb2-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="c1eb2-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1eb2-147">Next steps</span></span>

<span data-ttu-id="c1eb2-148">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) Aby dowiedzieć się więcej na temat grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c1eb2-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












