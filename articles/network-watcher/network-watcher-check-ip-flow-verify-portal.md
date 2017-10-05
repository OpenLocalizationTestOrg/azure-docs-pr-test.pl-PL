---
title: "Sprawdź ruchu z adresem IP obserwatora sieci Azure przepływ weryfikacji - portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób sprawdzania, jeśli ruch do i z maszyny wirtualnej jest dozwolona lub odmowa"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="a5301-103">Sprawdź, czy ruch jest dozwolony lub odmowa dostępu do lub z maszyny Wirtualnej z przepływem Sprawdź IP składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="a5301-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a5301-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a5301-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="a5301-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5301-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="a5301-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="a5301-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="a5301-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="a5301-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="a5301-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="a5301-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="a5301-109">Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który pozwala sprawdzić, jeśli ruch jest dozwolony na lub z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5301-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="a5301-110">Sprawdzanie poprawności może zostać uruchomione dla ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="a5301-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="a5301-111">Ten scenariusz przydaje się pobrać bieżący stan tego, czy maszyna wirtualna może komunikować się zasób zewnętrzny lub innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a5301-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="a5301-112">Sprawdź przepływ IP pozwala sprawdzić, czy reguł sieciowej grupy zabezpieczeń (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="a5301-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="a5301-113">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź jest zapewnienie ruchu, który ma być zablokowana jest prawidłowo blokowane przez grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="a5301-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a5301-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a5301-114">Before you begin</span></span>

<span data-ttu-id="a5301-115">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) do tworzenia obserwatora sieciowego lub mieć istniejące wystąpienie obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="a5301-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="a5301-116">Scenariusz również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje ma być używany.</span><span class="sxs-lookup"><span data-stu-id="a5301-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a5301-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="a5301-117">Scenario</span></span>

<span data-ttu-id="a5301-118">W tym scenariuszu IP przepływu Sprawdź, aby sprawdzić, jeśli maszyny wirtualnej mogą komunikować się z innego komputera za pośrednictwem portu 443.</span><span class="sxs-lookup"><span data-stu-id="a5301-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="a5301-119">Jeśli ruch jest niedozwolone, zwraca zasady zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="a5301-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="a5301-120">Aby dowiedzieć się więcej o Sprawdź przepływ IP, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a5301-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="a5301-121">Sprawdź uruchomienia przepływu IP</span><span class="sxs-lookup"><span data-stu-id="a5301-121">Run IP flow verify</span></span>

<span data-ttu-id="a5301-122">Przejdź do Twojej obserwatora sieciowego i kliknij **Sprawdź przepływ IP**.</span><span class="sxs-lookup"><span data-stu-id="a5301-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="a5301-123">Wybierz maszynę wirtualną i chcesz sprawdzić ruch z interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="a5301-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="a5301-124">Wprowadź wszelkie dodatkowe informacje filtrowania, a następnie kliknij przycisk **Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="a5301-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="a5301-125">Po kliknięciu **Sprawdź**, zaznaczono przepływem na podstawie podanych kryteriów.</span><span class="sxs-lookup"><span data-stu-id="a5301-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="a5301-126">Wynik jest **dozwolony dostęp do** lub **odmowa dostępu**.</span><span class="sxs-lookup"><span data-stu-id="a5301-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="a5301-127">W przypadku odmowy dostępu jest dostarczany zasady grupy zabezpieczeń sieci (NSG) i zabezpieczeń, która blokowania ruchu.</span><span class="sxs-lookup"><span data-stu-id="a5301-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="a5301-128">Jeśli odmowa ruchu jest oczekiwane zachowanie, reguła zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a5301-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="a5301-129">Sprawdź przepływ IP wymaga, aby zasobu maszyny Wirtualnej jest przydzielona.</span><span class="sxs-lookup"><span data-stu-id="a5301-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="a5301-130">Jak widać na poniższej ilustracji, zezwolono na ruch wychodzący protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a5301-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![Przepływ IP Sprawdź — omówienie][1]

<span data-ttu-id="a5301-132">Jak pokazano na poniższej ilustracji, ruch jest zmieniana na ruchu przychodzącego i portu wejściowego do 123.</span><span class="sxs-lookup"><span data-stu-id="a5301-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="a5301-133">Ruch teraz odmówiono, komunikat "Odmowa dostępu" jest dostępne oraz sieci zabezpieczeń grupy i zabezpieczeń reguła odmowy ruchu.</span><span class="sxs-lookup"><span data-stu-id="a5301-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![wyniki przepływu IP][2]

## <a name="next-steps"></a><span data-ttu-id="a5301-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5301-135">Next steps</span></span>

<span data-ttu-id="a5301-136">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) śledzić reguły zabezpieczeń sieciowych grupy i zabezpieczeń zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="a5301-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













