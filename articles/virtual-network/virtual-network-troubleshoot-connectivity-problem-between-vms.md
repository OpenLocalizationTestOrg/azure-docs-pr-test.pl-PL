---
title: "problemy z łącznością aaaTroubleshooting między maszynami wirtualnymi Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooTroubleshoot hello występują problemy z łącznością między maszynami wirtualnymi Azure."
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
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="b3d88-103">Rozwiązywanie problemów z łącznością między maszynami wirtualnymi Azure</span><span class="sxs-lookup"><span data-stu-id="b3d88-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="b3d88-104">Mogą wystąpić problemy z łącznością między maszynami wirtualnymi Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d88-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="b3d88-105">Ten artykuł zawiera toohelp kroki rozwiązywania problemów możesz rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="b3d88-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="b3d88-106">Objaw</span><span class="sxs-lookup"><span data-stu-id="b3d88-106">Symptom</span></span>

<span data-ttu-id="b3d88-107">Maszyny Wirtualnej platformy Azure nie może połączyć tooanother maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d88-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="b3d88-108">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="b3d88-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="b3d88-109">Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane</span><span class="sxs-lookup"><span data-stu-id="b3d88-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="b3d88-110">Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez</span><span class="sxs-lookup"><span data-stu-id="b3d88-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="b3d88-111">Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3d88-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="b3d88-112">Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie hello</span><span class="sxs-lookup"><span data-stu-id="b3d88-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="b3d88-113">Sprawdź, czy przyczyną problemu hello jest SNAT</span><span class="sxs-lookup"><span data-stu-id="b3d88-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="b3d88-114">Sprawdź, czy ruch jest blokowany przez listy kontroli dostępu dla hello klasyczne maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3d88-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="b3d88-115">Sprawdź czy punkt końcowy hello jest tworzone dla hello klasyczne maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3d88-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="b3d88-116">Udział sieciowy maszyny Wirtualnej tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="b3d88-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="b3d88-117">Łączność między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="b3d88-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="b3d88-118">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="b3d88-118">Troubleshooting steps</span></span>

<span data-ttu-id="b3d88-119">Wykonaj te kroki tootroubleshoot hello problem.</span><span class="sxs-lookup"><span data-stu-id="b3d88-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="b3d88-120">Sprawdź, czy hello problem zostanie rozwiązany po każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="b3d88-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="b3d88-121">Krok 1: Sprawdź, jeśli karta sieciowa jest błędnie skonfigurowane</span><span class="sxs-lookup"><span data-stu-id="b3d88-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="b3d88-122">Postępuj zgodnie z [jak tooreset interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="b3d88-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="b3d88-123">Jeśli wystąpi problem powitania po zmodyfikowaniu hello interfejsu sieciowego (NIC), wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b3d88-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="b3d88-124">**Karta sieciowa Mulit maszyny wirtualne**</span><span class="sxs-lookup"><span data-stu-id="b3d88-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="b3d88-125">Dodaj kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="b3d88-125">Add a NIC.</span></span>
2. <span data-ttu-id="b3d88-126">Rozwiąż problemy hello w hello zły karty Sieciowej lub usuwanie nieprawidłowych karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="b3d88-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="b3d88-127">Następnie readd hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="b3d88-127">Then readd hello NIC.</span></span>

<span data-ttu-id="b3d88-128">Aby uzyskać więcej informacji, zobacz [tooor interfejsów sieciowych Add usunięcia z maszyn wirtualnych](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b3d88-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="b3d88-129">**Wirtualna karta sieciowa na jednym**</span><span class="sxs-lookup"><span data-stu-id="b3d88-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="b3d88-130">Wdrożenie maszyny Wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="b3d88-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="b3d88-131">Wdrożenie maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b3d88-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="b3d88-132">Krok 2: Sprawdź, czy ruch sieciowy jest blokowany przez NSG lub przez</span><span class="sxs-lookup"><span data-stu-id="b3d88-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="b3d88-133">Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify, jeśli istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu.</span><span class="sxs-lookup"><span data-stu-id="b3d88-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="b3d88-134">Krok 3: Sprawdź, czy ruch sieciowy jest blokowany przez zaporę maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3d88-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="b3d88-135">Wyłącz hello zapory, a następnie hello wyniku testu.</span><span class="sxs-lookup"><span data-stu-id="b3d88-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="b3d88-136">Jeśli hello problem zostanie rozwiązany, sprawdź poprawność ustawień hello w zaporze hello i ponownie włącz.</span><span class="sxs-lookup"><span data-stu-id="b3d88-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="b3d88-137">Krok 4: Sprawdź, czy maszyna wirtualna aplikacji lub usługi nasłuchuje na porcie hello</span><span class="sxs-lookup"><span data-stu-id="b3d88-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="b3d88-138">Można użyć jednej z hello następujące metody toocheck, czy aplikacja wirtualna lub usługa nasłuchuje na porcie hello</span><span class="sxs-lookup"><span data-stu-id="b3d88-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="b3d88-139">Uruchom następujące polecenia toocheck czy hello server nasłuchuje na tym porcie hello.</span><span class="sxs-lookup"><span data-stu-id="b3d88-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="b3d88-140">**Maszyna wirtualna z systemem Windows**</span><span class="sxs-lookup"><span data-stu-id="b3d88-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="b3d88-141">**Maszyna wirtualna z systemem Linux**</span><span class="sxs-lookup"><span data-stu-id="b3d88-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="b3d88-142">Uruchom hello **Telnet** na powitania port hello tootest tooitself maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3d88-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="b3d88-143">Jeśli hello test zakończy się niepowodzeniem, aplikacja lub usługa nie jest skonfigurowany toolisten na porcie hello.</span><span class="sxs-lookup"><span data-stu-id="b3d88-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="b3d88-144">Krok 5: Sprawdź, czy przyczyną problemu hello jest SNAT</span><span class="sxs-lookup"><span data-stu-id="b3d88-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="b3d88-145">W niektórych scenariuszach hello maszyny Wirtualnej znajduje się za rozwiązania równoważenia obciążenia, które ma zależności zasobów poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d88-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="b3d88-146">W tych scenariuszach występują sporadyczne problemy z połączeniem, hello przyczyną problemu może być [wyczerpania portu SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="b3d88-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="b3d88-147">tooresolve hello problem, Utwórz VIP (lub ILPIP klasycznego) dla każdej maszyny Wirtualnej, która jest za usługą równoważenia obciążenia hello i zabezpieczyć za pomocą NSG lub listy ACL.</span><span class="sxs-lookup"><span data-stu-id="b3d88-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="b3d88-148">Krok 6: Sprawdź czy ruch jest blokowany przez listy kontroli dostępu dla tekst hello klasyczne maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3d88-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="b3d88-149">Listy ACL zapewnia hello możliwości tooselectively zezwolenia lub odmowy ruchu dla punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3d88-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="b3d88-150">Aby uzyskać więcej informacji, zobacz [Zarządzaj hello listy ACL punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="b3d88-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="b3d88-151">Krok 7: Sprawdź czy punkt końcowy hello jest tworzone dla tekst hello klasyczne maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3d88-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="b3d88-152">Wszystkie maszyny wirtualne utworzone na platformie Azure przy użyciu hello klasycznego modelu wdrażania może komunikować się automatycznie kanałem sieci prywatnej innym maszynom wirtualnym w hello się, że takie same w chmurze, usługi lub wirtualnych sieci.</span><span class="sxs-lookup"><span data-stu-id="b3d88-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="b3d88-153">Jednak komputery w innych sieciach wirtualnych wymagają punkty końcowe toodirect hello ruchu przychodzącego ruchu tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3d88-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="b3d88-154">Aby uzyskać więcej informacji, zobacz [jak tooset się punkty końcowe](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="b3d88-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="b3d88-155">Krok 8: Udział sieciowy maszyny Wirtualnej tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="b3d88-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="b3d88-156">W przypadku udziału sieciowego maszyny Wirtualnej tooa tooconnect hello problemu może być spowodowane niedostępny karty sieciowe w hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3d88-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="b3d88-157">toodelete hello niedostępny kart sieciowych, zobacz [jak toodelete hello niedostępny kart sieciowych](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="b3d88-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="b3d88-158">Krok 9: Łączności między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="b3d88-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="b3d88-159">Korzystanie z [Sprawdź przepływ IP obserwatora sieciowego](../network-watcher/network-watcher-ip-flow-verify-overview.md) i [rejestrowania przepływu NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify, jeśli istnieje grupa zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, która jest zakłócać przepływ ruchu.</span><span class="sxs-lookup"><span data-stu-id="b3d88-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="b3d88-160">Można również sprawdzić poprawności konfiguracji sieci wirtualnej między [tutaj](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="b3d88-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="b3d88-161">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="b3d88-161">Need help?</span></span> <span data-ttu-id="b3d88-162">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="b3d88-162">Contact support.</span></span>
<span data-ttu-id="b3d88-163">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="b3d88-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
