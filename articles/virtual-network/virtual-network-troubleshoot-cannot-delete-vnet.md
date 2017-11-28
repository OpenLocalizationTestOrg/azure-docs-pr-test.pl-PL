---
title: "aaaCannot usunąć sieci wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot hello problem, w której nie można usunąć sieci wirtualnej na platformie Azure."
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
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="256b8-103">Rozwiązywanie problemów: Nie powiodło się toodelete sieci wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="256b8-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="256b8-104">Błędy może pojawić się podczas próby toodelete sieci wirtualnej na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="256b8-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="256b8-105">Ten artykuł zawiera toohelp kroki rozwiązywania problemów możesz rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="256b8-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="256b8-106">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="256b8-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="256b8-107">[Sprawdź, czy brama sieci wirtualnej jest uruchomiony w sieci wirtualnej hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="256b8-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="256b8-108">[Sprawdź, czy bramę aplikacji jest uruchomiony w sieci wirtualnej hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="256b8-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="256b8-109">[Sprawdź, czy usługi Azure Active Directory domeny jest włączone w sieci wirtualnej hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="256b8-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="256b8-110">[Sprawdź, czy sieć wirtualna hello zasobów połączonych tooother](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="256b8-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="256b8-111">[Sprawdź, czy maszyna wirtualna nadal działa w sieci wirtualnej hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="256b8-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="256b8-112">[Sprawdź, czy sieć wirtualna hello utkwiła w automatycznej migracji](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="256b8-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="256b8-113">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="256b8-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="256b8-114">Sprawdź, czy brama sieci wirtualnej jest uruchomiony w sieci wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="256b8-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="256b8-115">tooremove hello sieci wirtualnej, należy najpierw usunąć hello bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="256b8-116">Dla klasycznych sieci wirtualnych, przejdź toohello **omówienie** strony hello klasycznej sieci wirtualnej w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="256b8-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="256b8-117">W hello **połączeń sieci VPN** sekcji, jeśli hello brama jest uruchomiona w sieci wirtualnej hello, zobaczysz hello IP adres bramy hello.</span><span class="sxs-lookup"><span data-stu-id="256b8-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Sprawdź, czy brama jest uruchomiona](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="256b8-119">Dla sieci wirtualnych, przejdź toohello **omówienie** strony hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="256b8-120">Sprawdź **urządzeń podłączonych** hello bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Sprawdź hello podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="256b8-122">Zanim będzie można usunąć bramy hello, najpierw usuń wszystkie **połączenia** obiektów w hello bramy.</span><span class="sxs-lookup"><span data-stu-id="256b8-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="256b8-123">Sprawdź, czy w sieci wirtualnej hello działa bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="256b8-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="256b8-124">Przejdź toohello **omówienie** strony hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="256b8-125">Sprawdź hello **urządzeń podłączonych** hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="256b8-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Sprawdź hello podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="256b8-127">W przypadku bramy aplikacji, należy usunąć przed usunięciem hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="256b8-128">Sprawdź, czy w sieci wirtualnej hello jest włączone usług domenowych Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="256b8-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="256b8-129">Jeśli hello usług domenowych w usłudze Active Directory jest włączone i połączone toohello sieci wirtualnej, nie można usunąć tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Sprawdź hello podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="256b8-131">toodisable hello usługi, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="256b8-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="256b8-132">Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="256b8-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="256b8-133">Wybierz w okienku po lewej stronie powitania **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="256b8-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="256b8-134">Wybierz katalog usługi Azure Active Directory (Azure AD) hello, który ma usług domenowych Active Directory włączone.</span><span class="sxs-lookup"><span data-stu-id="256b8-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="256b8-135">Wybierz hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="256b8-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="256b8-136">W obszarze **usług domenowych w usłudze**, zmień hello **włączyć usługi domenowe dla tego katalogu** opcję zbyt**nr**.</span><span class="sxs-lookup"><span data-stu-id="256b8-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="256b8-137">Sprawdź, czy sieć wirtualna hello tooother połączonych zasobów</span><span class="sxs-lookup"><span data-stu-id="256b8-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="256b8-138">Sprawdź, czy łącza obwód, połączeń i komunikacji równorzędnych sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="256b8-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="256b8-139">Żadnego z nich może spowodować toofail usunięcia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="256b8-140">Witaj kolejność usuwania zalecana jest następująca:</span><span class="sxs-lookup"><span data-stu-id="256b8-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="256b8-141">Połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="256b8-141">Gateway connections</span></span>
2. <span data-ttu-id="256b8-142">Bramy</span><span class="sxs-lookup"><span data-stu-id="256b8-142">Gateways</span></span>
3. <span data-ttu-id="256b8-143">Adresy IP</span><span class="sxs-lookup"><span data-stu-id="256b8-143">IPs</span></span>
4. <span data-ttu-id="256b8-144">Komunikacji równorzędnych sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="256b8-144">Virtual network peerings</span></span>
5. <span data-ttu-id="256b8-145">Środowisko usługi aplikacji (ASE)</span><span class="sxs-lookup"><span data-stu-id="256b8-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="256b8-146">Sprawdź, czy maszyna wirtualna nadal działa w sieci wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="256b8-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="256b8-147">Upewnij się, nieprawidłowość w sieci wirtualnej hello żadnej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="256b8-148">Sprawdź, czy sieć wirtualna hello utkwiła w automatycznej migracji</span><span class="sxs-lookup"><span data-stu-id="256b8-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="256b8-149">Jeśli w sieci wirtualnej hello jest zablokowana w stanie migracji, nie można usunąć.</span><span class="sxs-lookup"><span data-stu-id="256b8-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="256b8-150">Uruchom następujące polecenia tooabort hello migracji hello, a następnie usuń hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="256b8-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="256b8-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="256b8-151">Next steps</span></span>

- [<span data-ttu-id="256b8-152">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="256b8-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="256b8-153">Często zadawane pytania dotyczące sieci wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="256b8-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)