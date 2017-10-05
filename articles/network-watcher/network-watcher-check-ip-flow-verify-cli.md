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
ms.openlocfilehash: 0b52257a6c38a4392573672b7190d2269c2f145a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="e7687-103">Sprawdź, czy ruch jest dozwolony lub odmowa dostępu do lub z maszyny Wirtualnej z przepływem Sprawdź IP składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="e7687-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e7687-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e7687-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="e7687-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7687-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="e7687-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="e7687-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="e7687-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="e7687-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="e7687-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="e7687-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="e7687-109">Przepływ IP Sprawdź jest funkcją obserwatora sieciowego, który pozwala sprawdzić, jeśli ruch jest dozwolony na lub z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e7687-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="e7687-110">Ten scenariusz przydaje się pobrać bieżący stan tego, czy maszyny wirtualne mogą komunikować się z zasobu zewnętrznego i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e7687-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="e7687-111">Sprawdź przepływ IP pozwala sprawdzić, czy reguł sieciowej grupy zabezpieczeń (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="e7687-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="e7687-112">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź jest zapewnienie ruchu, który ma być zablokowana jest prawidłowo blokowane przez grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="e7687-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="e7687-113">W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania zarządzania zasobów, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="e7687-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="e7687-114">Aby wykonać kroki opisane w tym artykule, należy [instalowanie interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e7687-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e7687-115">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e7687-115">Before you begin</span></span>

<span data-ttu-id="e7687-116">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) do tworzenia obserwatora sieciowego lub mieć istniejące wystąpienie obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="e7687-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="e7687-117">Scenariusz również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje ma być używany.</span><span class="sxs-lookup"><span data-stu-id="e7687-117">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="e7687-118">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="e7687-118">Scenario</span></span>

<span data-ttu-id="e7687-119">W tym scenariuszu IP przepływu Sprawdź, aby sprawdzić, czy maszyna wirtualna może komunikować się znanego adresu IP usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="e7687-119">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="e7687-120">Jeśli ruch jest niedozwolone, zwraca zasady zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="e7687-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="e7687-121">Aby dowiedzieć się więcej o Sprawdź przepływ IP, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e7687-121">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="e7687-122">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e7687-122">Get a VM</span></span>

<span data-ttu-id="e7687-123">Przepływ IP Sprawdź testy ruchu do lub z adresu IP na maszynie wirtualnej lub zdalnego miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="e7687-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="e7687-124">Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e7687-124">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="e7687-125">Jeśli znasz już identyfikator maszyny wirtualnej do użycia, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="e7687-125">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a><span data-ttu-id="e7687-126">Pobierz karty interfejsu Sieciowego</span><span class="sxs-lookup"><span data-stu-id="e7687-126">Get the NICS</span></span>

<span data-ttu-id="e7687-127">Adres IP karty sieciowej na maszynie wirtualnej jest potrzebne w tym przykładzie Pobieramy kart sieciowych w maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e7687-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="e7687-128">Jeśli znasz już adres IP, który ma zostać przetestowana na maszynie wirtualnej, można pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="e7687-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="e7687-129">Sprawdź uruchomienia przepływu IP</span><span class="sxs-lookup"><span data-stu-id="e7687-129">Run IP flow verify</span></span>

<span data-ttu-id="e7687-130">Teraz, gdy mamy informacje potrzebne do uruchomienia polecenia cmdlet, możemy uruchomić `az network watcher test-ip-flow` polecenia cmdlet, aby przetestować ruchu.</span><span class="sxs-lookup"><span data-stu-id="e7687-130">Now that we have the information needed to run the cmdlet, we run the `az network watcher test-ip-flow` cmdlet to test the traffic.</span></span> <span data-ttu-id="e7687-131">W tym przykładzie użyto pierwszego adresu IP na pierwszej karcie sieciowej.</span><span class="sxs-lookup"><span data-stu-id="e7687-131">In this example, we are using the first IP address on the first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="e7687-132">Przepływ IP Sprawdź wymaga, aby zasobu maszyny Wirtualnej jest przydzielona do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e7687-132">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="e7687-133">Przejrzyj wyniki</span><span class="sxs-lookup"><span data-stu-id="e7687-133">Review Results</span></span>

<span data-ttu-id="e7687-134">Po uruchomieniu `az network watcher test-ip-flow` wyniki są zwracane, w poniższym przykładzie jest wyników zwróconych z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="e7687-134">After running `az network watcher test-ip-flow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="e7687-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7687-135">Next steps</span></span>

<span data-ttu-id="e7687-136">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) śledzić reguły zabezpieczeń sieciowych grupy i zabezpieczeń zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="e7687-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="e7687-137">Dowiedz się, jak inspekcji ustawienia grupy NSG, odwiedzając [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e7687-137">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
