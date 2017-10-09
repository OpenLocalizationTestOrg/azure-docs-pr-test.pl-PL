---
title: "Sprawdź aaaVerify ruchu z przepływem IP obserwatora sieci platformy Azure - REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub niedozwolony"
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
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="0fcbf-103">Sprawdź, czy ruch jest dozwolony lub odrzucany z przepływem IP Sprawdź składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="0fcbf-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0fcbf-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0fcbf-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="0fcbf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fcbf-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="0fcbf-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="0fcbf-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="0fcbf-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="0fcbf-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="0fcbf-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="0fcbf-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="0fcbf-109">Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="0fcbf-110">Sprawdzanie poprawności Hello mogą być uruchamiane dla ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="0fcbf-111">Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać tooan zasobu zewnętrznego i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="0fcbf-112">Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="0fcbf-113">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0fcbf-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="0fcbf-114">Before you begin</span></span>

<span data-ttu-id="0fcbf-115">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="0fcbf-116">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="0fcbf-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="0fcbf-117">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="0fcbf-118">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="0fcbf-118">Scenario</span></span>

<span data-ttu-id="0fcbf-119">W tym scenariuszu tooverify Sprawdź przepływ IP Jeśli maszynę wirtualną można rozmawiać tooanother komputera za pośrednictwem portu 443.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="0fcbf-120">Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="0fcbf-121">toolearn więcej informacji na temat przepływu IP upewnij się, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0fcbf-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="0fcbf-122">W tym scenariuszu należy:</span><span class="sxs-lookup"><span data-stu-id="0fcbf-122">In this scenario, you:</span></span>

* <span data-ttu-id="0fcbf-123">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0fcbf-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="0fcbf-124">Sprawdź połączenie IP przepływu</span><span class="sxs-lookup"><span data-stu-id="0fcbf-124">Call IP flow verify</span></span>
* <span data-ttu-id="0fcbf-125">Sprawdź wyniki</span><span class="sxs-lookup"><span data-stu-id="0fcbf-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="0fcbf-126">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="0fcbf-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="0fcbf-127">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0fcbf-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="0fcbf-128">Uruchom maszynę wirtualną powitania po tooreturn skryptu.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="0fcbf-129">Witaj następujący kod wymaga wartości zmiennych hello:</span><span class="sxs-lookup"><span data-stu-id="0fcbf-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="0fcbf-130">**Identyfikator subskrypcji** — Witaj toouse identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="0fcbf-131">**resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="0fcbf-132">Witaj informacje potrzebne jest hello identyfikator typu hello `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="0fcbf-133">Hello wyniki powinny być podobne toohello po przykładowym kodzie:</span><span class="sxs-lookup"><span data-stu-id="0fcbf-133">hello results should be similar toohello following code sample:</span></span>

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

## <a name="call-ip-flow-verify"></a><span data-ttu-id="0fcbf-134">Wywołanie IP przepływu Sprawdź</span><span class="sxs-lookup"><span data-stu-id="0fcbf-134">Call IP flow Verify</span></span>

<span data-ttu-id="0fcbf-135">Witaj poniższy przykład tworzy żądanie tooverify hello ruchu dla określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="0fcbf-136">odpowiedź Hello zwraca czy hello ruch jest dozwolony, czy ruch hello jest zabroniony.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="0fcbf-137">Jeśli ruch odmówiono ona również zwraca jakie bloków reguł hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="0fcbf-138">Sprawdź przepływ IP wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="0fcbf-139">skrypt Hello wymaga zasobów hello identyfikator maszyny wirtualnej i karty interfejsu sieciowego na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="0fcbf-140">Wartości te są dostarczane przez hello poprzedzających danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="0fcbf-141">Dla wszystkich pozostałych obserwatora sieciowego wywołania hello Nazwa grupy zasobów w żądaniu hello hello taką, która zawiera nie zasoby hello czynności diagnostyczne hello są wykonywane na powitania wystąpienia obserwatora sieciowego, to identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="0fcbf-142">Opis wyników hello</span><span class="sxs-lookup"><span data-stu-id="0fcbf-142">Understanding hello results</span></span>

<span data-ttu-id="0fcbf-143">odpowiedź Hello, wracając informuje, czy ruch hello jest dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="0fcbf-144">odpowiedź Hello wygląda jedną hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="0fcbf-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="0fcbf-145">**Dozwolone**</span><span class="sxs-lookup"><span data-stu-id="0fcbf-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="0fcbf-146">**Odmowa dostępu**</span><span class="sxs-lookup"><span data-stu-id="0fcbf-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="0fcbf-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fcbf-147">Next steps</span></span>

<span data-ttu-id="0fcbf-148">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn więcej informacji na temat grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="0fcbf-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












