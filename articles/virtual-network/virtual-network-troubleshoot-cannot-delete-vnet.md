---
title: "Nie można usunąć sieci wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązać ten problem, w której nie można usunąć sieci wirtualnej na platformie Azure."
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
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="61cd1-103">Rozwiązywanie problemów: Nie można usunąć sieci wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="61cd1-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="61cd1-104">Błędy może pojawić się podczas próby usunięcia sieci wirtualnej na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="61cd1-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="61cd1-105">Ten artykuł zawiera kroki rozwiązywania problemów, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="61cd1-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="61cd1-106">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="61cd1-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="61cd1-107">[Sprawdź, czy brama sieci wirtualnej jest uruchomiony w sieci wirtualnej](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="61cd1-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="61cd1-108">[Sprawdź, czy bramę aplikacji jest uruchomiony w sieci wirtualnej](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="61cd1-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="61cd1-109">[Sprawdź, czy usługi Azure Active Directory domeny jest włączone w sieci wirtualnej](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="61cd1-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="61cd1-110">[Sprawdź, czy sieci wirtualnej jest podłączona do innego zasobu](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="61cd1-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="61cd1-111">[Sprawdź, czy maszyna wirtualna nadal działa w sieci wirtualnej](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="61cd1-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="61cd1-112">[Sprawdź, czy sieć wirtualna utkwiła w automatycznej migracji](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="61cd1-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="61cd1-113">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="61cd1-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="61cd1-114">Sprawdź, czy brama sieci wirtualnej jest uruchomiony w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61cd1-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="61cd1-115">Aby usunąć sieci wirtualnej, należy najpierw usunąć bramę sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="61cd1-116">Aby klasycznych sieci wirtualnych, przejdź do tematu **omówienie** strony klasycznej sieci wirtualnej w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="61cd1-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="61cd1-117">W **połączeń sieci VPN** sekcji, jeśli brama jest uruchomiona w sieci wirtualnej, zostanie wyświetlony adres IP bramy.</span><span class="sxs-lookup"><span data-stu-id="61cd1-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![Sprawdź, czy brama jest uruchomiona](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="61cd1-119">Dla sieci wirtualnych, przejdź do **omówienie** strony sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="61cd1-120">Sprawdź **urządzeń podłączonych** dla bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-120">Check **Connected devices** for the virtual network gateway.</span></span>

![Sprawdź podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="61cd1-122">Zanim będzie można usunąć bramy, najpierw usuń wszystkie **połączenia** obiektów w bramie.</span><span class="sxs-lookup"><span data-stu-id="61cd1-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="61cd1-123">Sprawdź, czy w sieci wirtualnej jest uruchomiona bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="61cd1-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="61cd1-124">Przejdź do **omówienie** strony sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="61cd1-125">Sprawdź **urządzeń podłączonych** bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="61cd1-125">Check the **Connected devices** for the application gateway.</span></span>

![Sprawdź podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="61cd1-127">W przypadku bramy aplikacji, należy go usunąć przed usunięciem sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="61cd1-128">Sprawdź, czy usługi Azure Active Directory domeny jest włączone w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61cd1-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="61cd1-129">Jeśli usług domenowych w usłudze Active Directory jest włączony i podłączony do sieci wirtualnej, nie można usunąć tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![Sprawdź podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="61cd1-131">Aby wyłączyć usługę, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="61cd1-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="61cd1-132">Przejdź do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="61cd1-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="61cd1-133">W okienku po lewej stronie wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61cd1-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="61cd1-134">Wybierz katalog usługi Azure Active Directory (Azure AD), który ma usług domenowych Active Directory włączone.</span><span class="sxs-lookup"><span data-stu-id="61cd1-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="61cd1-135">Wybierz kartę **Konfigurowanie**.</span><span class="sxs-lookup"><span data-stu-id="61cd1-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="61cd1-136">W obszarze **usług domenowych w usłudze**, zmień **włączyć usługi domenowe dla tego katalogu** opcji w celu **nr**.</span><span class="sxs-lookup"><span data-stu-id="61cd1-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="61cd1-137">Sprawdź, czy sieci wirtualnej jest podłączona do innego zasobu</span><span class="sxs-lookup"><span data-stu-id="61cd1-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="61cd1-138">Sprawdź, czy łącza obwód, połączeń i komunikacji równorzędnych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="61cd1-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="61cd1-139">Żadnego z tych adresów może spowodować niepowodzenie usunięcie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="61cd1-140">Kolejność usuwania zalecana jest następująca:</span><span class="sxs-lookup"><span data-stu-id="61cd1-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="61cd1-141">Połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="61cd1-141">Gateway connections</span></span>
2. <span data-ttu-id="61cd1-142">Bramy</span><span class="sxs-lookup"><span data-stu-id="61cd1-142">Gateways</span></span>
3. <span data-ttu-id="61cd1-143">Adresy IP</span><span class="sxs-lookup"><span data-stu-id="61cd1-143">IPs</span></span>
4. <span data-ttu-id="61cd1-144">Komunikacji równorzędnych sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="61cd1-144">Virtual network peerings</span></span>
5. <span data-ttu-id="61cd1-145">Środowisko usługi aplikacji (ASE)</span><span class="sxs-lookup"><span data-stu-id="61cd1-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="61cd1-146">Sprawdź, czy maszyna wirtualna nadal działa w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61cd1-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="61cd1-147">Upewnij się, że żadna maszyna wirtualna będzie w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="61cd1-148">Sprawdź, czy utkwiła w automatycznej migracji sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61cd1-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="61cd1-149">Jeśli sieć wirtualna jest zablokowana w stanie migracji, nie można usunąć.</span><span class="sxs-lookup"><span data-stu-id="61cd1-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="61cd1-150">Uruchom następujące polecenie, aby przerwać migracji, a następnie usunąć sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61cd1-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="61cd1-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61cd1-151">Next steps</span></span>

- [<span data-ttu-id="61cd1-152">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="61cd1-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="61cd1-153">Często zadawane pytania dotyczące sieci wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="61cd1-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)