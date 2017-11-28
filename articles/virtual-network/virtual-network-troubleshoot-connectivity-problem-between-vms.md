---
title: "Rozwiązywanie problemów z łącznością między maszynami wirtualnymi Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywać problemy z łącznością między maszynami wirtualnymi Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="3898f-103">Rozwiązywanie problemów z łącznością między maszynami wirtualnymi Azure</span><span class="sxs-lookup"><span data-stu-id="3898f-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="3898f-104">Mogą wystąpić problemy z łącznością między maszynami wirtualnymi Azure.</span><span class="sxs-lookup"><span data-stu-id="3898f-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="3898f-105">Ten artykuł zawiera kroki rozwiązywania problemów, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="3898f-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="3898f-106">Objaw</span><span class="sxs-lookup"><span data-stu-id="3898f-106">Symptom</span></span>

<span data-ttu-id="3898f-107">Maszyny Wirtualnej platformy Azure nie może połączyć się innej maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3898f-107">An Azure VM cannot connect to another Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="3898f-108">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="3898f-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="3898f-109">Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane</span><span class="sxs-lookup"><span data-stu-id="3898f-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="3898f-110">Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez</span><span class="sxs-lookup"><span data-stu-id="3898f-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="3898f-111">Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="3898f-112">Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie</span><span class="sxs-lookup"><span data-stu-id="3898f-112">Check whether VM app or service is listening on the port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="3898f-113">Sprawdź, czy przyczyną problemu jest SNAT</span><span class="sxs-lookup"><span data-stu-id="3898f-113">Check whether the problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="3898f-114">Sprawdź, czy ruch jest blokowany przez listy kontroli dostępu dla klasycznego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-114">Check whether traffic is blocked by ACLs for the classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="3898f-115">Sprawdź, czy punkt końcowy jest tworzony dla klasycznego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-115">Check whether the endpoint is created for the classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="3898f-116">Nie można nawiązać połączenia z udziału sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-116">Unable to connect to a VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="3898f-117">Łączność między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="3898f-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="3898f-118">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="3898f-118">Troubleshooting steps</span></span>

<span data-ttu-id="3898f-119">Wykonaj następujące kroki, aby rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="3898f-119">Follow these steps to troubleshoot the problem.</span></span> <span data-ttu-id="3898f-120">Sprawdź, czy problem został rozwiązany po każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="3898f-120">Check whether the problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="3898f-121">Krok 1: Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane</span><span class="sxs-lookup"><span data-stu-id="3898f-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="3898f-122">Postępuj zgodnie z [sposób resetowania interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="3898f-122">Follow [How to reset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="3898f-123">Jeśli ten problem występuje po zmodyfikowaniu interfejsu sieciowego (NIC), wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3898f-123">If the problem occurs after you modify the network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="3898f-124">**Karta sieciowa Mulit maszyny wirtualne**</span><span class="sxs-lookup"><span data-stu-id="3898f-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="3898f-125">Dodaj kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="3898f-125">Add a NIC.</span></span>
2. <span data-ttu-id="3898f-126">Rozwiąż problemy w zły karty Sieciowej lub usunąć zły karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="3898f-126">Fix the problems in the bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="3898f-127">Następnie readd karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="3898f-127">Then readd the NIC.</span></span>

<span data-ttu-id="3898f-128">Aby uzyskać więcej informacji, zobacz [interfejsów sieciowych, aby dodać lub usunąć z maszyny wirtualnej](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="3898f-128">For more information, see [Add network interfaces to or remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="3898f-129">**Wirtualna karta sieciowa na jednym**</span><span class="sxs-lookup"><span data-stu-id="3898f-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="3898f-130">Wdrożenie maszyny Wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="3898f-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="3898f-131">Wdrożenie maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3898f-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="3898f-132">Krok 2: Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez</span><span class="sxs-lookup"><span data-stu-id="3898f-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="3898f-133">Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) do ustalenia, czy istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu.</span><span class="sxs-lookup"><span data-stu-id="3898f-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="3898f-134">Krok 3: Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="3898f-135">Wyłącz zaporę, a następnie sprawdź wynik.</span><span class="sxs-lookup"><span data-stu-id="3898f-135">Disable the firewall, and then test the result.</span></span> <span data-ttu-id="3898f-136">Jeśli ten problem zostanie rozwiązany, sprawdź poprawność ustawień zapory, a następnie ponownie włącz.</span><span class="sxs-lookup"><span data-stu-id="3898f-136">If the problem is resolved, validate the settings in the firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a><span data-ttu-id="3898f-137">Krok 4: Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie</span><span class="sxs-lookup"><span data-stu-id="3898f-137">Step 4: Check whether VM app or service is listening on the port</span></span>

<span data-ttu-id="3898f-138">Można użyć jednej z następujących metod do sprawdzenia, czy aplikacja wirtualna lub usługa nasłuchuje na porcie</span><span class="sxs-lookup"><span data-stu-id="3898f-138">You can use one of the following methods to check whether VM Application or Service is listening on the port</span></span>

- <span data-ttu-id="3898f-139">Uruchom następujące polecenia, aby sprawdzić, czy serwer nasłuchuje na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="3898f-139">Run the following commands to check whether the server is listening on that port.</span></span>

<span data-ttu-id="3898f-140">**Maszyna wirtualna z systemem Windows**</span><span class="sxs-lookup"><span data-stu-id="3898f-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="3898f-141">**Maszyna wirtualna z systemem Linux**</span><span class="sxs-lookup"><span data-stu-id="3898f-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="3898f-142">Uruchom **Telnet** polecenia na maszynie Wirtualnej do samej siebie, aby przetestować portu.</span><span class="sxs-lookup"><span data-stu-id="3898f-142">Run the **Telnet** command on the VM to itself to test the port.</span></span> <span data-ttu-id="3898f-143">Jeśli test ma wynik negatywny, aplikacja lub usługa nie skonfigurowano nasłuchiwanie na porcie.</span><span class="sxs-lookup"><span data-stu-id="3898f-143">If the test fails, application or service is not configured to listen on the port.</span></span>

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a><span data-ttu-id="3898f-144">Krok 5: Sprawdź, czy przyczyną problemu jest SNAT</span><span class="sxs-lookup"><span data-stu-id="3898f-144">Step 5: Check whether the problem is caused by SNAT</span></span>

<span data-ttu-id="3898f-145">W niektórych scenariuszach maszyna wirtualna znajduje się za rozwiązania równoważenia obciążenia, które ma zależności zasobów poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="3898f-145">In some scenarios, the VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="3898f-146">W tych scenariuszach występują sporadyczne problemy z połączeniem, problem może być spowodowane [wyczerpania portu SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="3898f-146">In these scenarios, if you experience intermittent connection problems, the problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="3898f-147">Aby rozwiązać ten problem, Utwórz dla każdej maszyny Wirtualnej związanej z modułem równoważenia obciążenia i zabezpieczyć za pomocą NSG lub listy ACL adresu VIP (lub ILPIP klasycznego).</span><span class="sxs-lookup"><span data-stu-id="3898f-147">To resolve the issue, create a VIP (or ILPIP for classic) for each VM that is behind the Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a><span data-ttu-id="3898f-148">Krok 6: Sprawdź, czy ruch jest blokowany przez listy kontroli dostępu dla klasycznego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-148">Step 6: Check whether traffic is blocked by ACLs for the classic VM</span></span>

<span data-ttu-id="3898f-149">Listy ACL zapewnia możliwość selektywnego akceptowanie lub odrzucanie ruchu dla punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3898f-149">An ACL provides the ability to selectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="3898f-150">Aby uzyskać więcej informacji, zobacz [Zarządzanie listy ACL punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="3898f-150">For more information, see [Manage the ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a><span data-ttu-id="3898f-151">Krok 7: Sprawdź, czy punkt końcowy jest tworzony dla klasycznego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-151">Step 7: Check whether the endpoint is created for the classic VM</span></span>

<span data-ttu-id="3898f-152">Wszystkie maszyny wirtualne utworzone na platformie Azure przy użyciu klasycznego modelu wdrażania można automatycznie komunikują się za pośrednictwem kanału między maszynami wirtualnymi w tej samej usługi w chmurze lub sieci wirtualnej sieci prywatnej.</span><span class="sxs-lookup"><span data-stu-id="3898f-152">All VMs that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="3898f-153">Jednak komputery w innych sieciach wirtualnych wymagają punktów końcowych, aby skierować ruch sieciowy przychodzący do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3898f-153">However, computers on other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="3898f-154">Aby uzyskać więcej informacji, zobacz [sposobu konfigurowania punktów końcowych](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="3898f-154">For more information, see [How to set up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a><span data-ttu-id="3898f-155">Krok 8: Nie można nawiązać połączenia z udziału sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="3898f-155">Step 8: Unable to connect to a VM network share</span></span>

<span data-ttu-id="3898f-156">Jeśli nie można nawiązać połączenia z udziału sieciowego maszyny Wirtualnej, problem może wpływać niedostępny kart sieciowych w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3898f-156">If you are unable to connect to a VM network share, the problem can be caused by unavailable NICs in the VM.</span></span> <span data-ttu-id="3898f-157">Aby usunąć niedostępny kart sieciowych, zobacz [sposób usuwania niedostępny kart sieciowych](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="3898f-157">To delete the unavailable NICs, see [How to delete the unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="3898f-158">Krok 9: Łączności między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="3898f-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="3898f-159">Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) do ustalenia, czy istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu.</span><span class="sxs-lookup"><span data-stu-id="3898f-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="3898f-160">Można również sprawdzić poprawności konfiguracji sieci wirtualnej między [tutaj](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="3898f-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="3898f-161">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="3898f-161">Need help?</span></span> <span data-ttu-id="3898f-162">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="3898f-162">Contact support.</span></span>
<span data-ttu-id="3898f-163">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="3898f-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>