---
title: "Weryfikacja ruchu Azure sieci obserwatora IP przepływ weryfikacji - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób sprawdzania, jeśli ruch do i z maszyny wirtualnej jest dozwolona lub odmowa przy użyciu wiersza polecenia platformy Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c5fe6c662b3ee2a443904b0f12cbfd495d9bc85e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="984a4-103">Sprawdź, czy ruch jest dozwolony lub odmowa dostępu do lub z maszyny Wirtualnej z przepływem Sprawdź IP składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="984a4-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="984a4-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="984a4-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="984a4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="984a4-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="984a4-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="984a4-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="984a4-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="984a4-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="984a4-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="984a4-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="984a4-109">Przepływ IP Sprawdź jest funkcją obserwatora sieciowego, który pozwala sprawdzić, jeśli ruch jest dozwolony na lub z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="984a4-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="984a4-110">Ten scenariusz przydaje się pobrać bieżący stan tego, czy maszyny wirtualne mogą komunikować się z zasobu zewnętrznego i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="984a4-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="984a4-111">Sprawdź przepływ IP pozwala sprawdzić, czy reguł sieciowej grupy zabezpieczeń (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="984a4-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="984a4-112">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź jest zapewnienie ruchu, który ma być zablokowana jest prawidłowo blokowane przez grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="984a4-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="984a4-113">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="984a4-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="984a4-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="984a4-114">Before you begin</span></span>

<span data-ttu-id="984a4-115">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) do tworzenia obserwatora sieciowego lub mieć istniejące wystąpienie obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="984a4-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="984a4-116">Scenariusz również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje ma być używany.</span><span class="sxs-lookup"><span data-stu-id="984a4-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="984a4-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="984a4-117">Scenario</span></span>

<span data-ttu-id="984a4-118">W tym scenariuszu IP przepływu Sprawdź, aby sprawdzić, czy maszyna wirtualna może komunikować się znanego adresu IP usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="984a4-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="984a4-119">Jeśli ruch jest niedozwolone, zwraca zasady zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="984a4-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="984a4-120">Aby dowiedzieć się więcej o Sprawdź przepływ IP, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="984a4-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="984a4-121">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="984a4-121">Get a VM</span></span>

<span data-ttu-id="984a4-122">Przepływ IP Sprawdź testy ruchu do lub z adresu IP na maszynie wirtualnej lub zdalnego miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="984a4-122">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="984a4-123">Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="984a4-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="984a4-124">Jeśli znasz już identyfikator maszyny wirtualnej do użycia, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="984a4-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a><span data-ttu-id="984a4-125">Pobierz karty interfejsu Sieciowego</span><span class="sxs-lookup"><span data-stu-id="984a4-125">Get the NICS</span></span>

<span data-ttu-id="984a4-126">Adres IP karty sieciowej na maszynie wirtualnej jest potrzebne w tym przykładzie Pobieramy kart sieciowych w maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="984a4-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="984a4-127">Jeśli znasz już adres IP, który ma zostać przetestowana na maszynie wirtualnej, można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="984a4-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="984a4-128">Sprawdź uruchomienia przepływu IP</span><span class="sxs-lookup"><span data-stu-id="984a4-128">Run IP flow verify</span></span>

<span data-ttu-id="984a4-129">Teraz, gdy mamy informacje potrzebne do uruchomienia polecenia cmdlet, możemy uruchomić `network watcher ip-flow-verify` polecenia cmdlet, aby przetestować ruchu.</span><span class="sxs-lookup"><span data-stu-id="984a4-129">Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic.</span></span> <span data-ttu-id="984a4-130">W tym przykładzie użyto pierwszego adresu IP na pierwszej karcie sieciowej.</span><span class="sxs-lookup"><span data-stu-id="984a4-130">In this example, we are using the first IP address on the first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="984a4-131">Przepływ IP Sprawdź wymaga, aby zasobu maszyny Wirtualnej jest przydzielona do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="984a4-131">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="984a4-132">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="984a4-132">Review Results</span></span>

<span data-ttu-id="984a4-133">Po uruchomieniu `network watcher ip-flow-verify` wyniki są zwracane, w poniższym przykładzie jest wyników zwróconych z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="984a4-133">After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="984a4-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="984a4-134">Next steps</span></span>

<span data-ttu-id="984a4-135">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) śledzić reguły zabezpieczeń sieciowych grupy i zabezpieczeń zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="984a4-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="984a4-136">Dowiedz się, jak inspekcji ustawienia grupy NSG, odwiedzając [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="984a4-136">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
