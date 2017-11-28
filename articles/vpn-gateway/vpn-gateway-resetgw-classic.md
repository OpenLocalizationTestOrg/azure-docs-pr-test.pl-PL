---
title: "Resetowanie bramy sieci VPN platformy Azure, aby ponownie ustanowić tuneli IPsec | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono Resetowanie bramy sieci VPN platformy Azure, aby ponownie ustanowić tuneli IPsec. Artykuł dotyczy bram sieci VPN w klasycznym i modeli wdrażania Menedżera zasobów."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 7c5ba9310568571991708ab54a5275df6ea84a39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="b453c-104">Resetowanie VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="b453c-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="b453c-105">Resetowanie bramy Azure VPN Gateway przydaje się w przypadku utraty połączenia sieci VPN obejmującego wiele lokalizacji w jednym lub wielu tunelach VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="b453c-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="b453c-106">W takiej sytuacji urządzenia lokalnej sieci VPN działają prawidłowo, ale nie mogą nawiązać połączenia w ramach tuneli używających protokołu IPsec z bramami sieci VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="b453c-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="b453c-107">Ten artykuł pomoże Ci zresetować bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="b453c-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="b453c-108">Co się dzieje podczas resetowania?</span><span class="sxs-lookup"><span data-stu-id="b453c-108">What happens during a reset?</span></span>

<span data-ttu-id="b453c-109">Brama sieci VPN składa się z dwóch wystąpień maszyn wirtualnych działających w konfiguracji aktywnego gotowości.</span><span class="sxs-lookup"><span data-stu-id="b453c-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="b453c-110">Zresetowanie bramy uruchamia bramy, a następnie ponownie stosuje konfiguracje między różnymi lokalizacjami, aby go.</span><span class="sxs-lookup"><span data-stu-id="b453c-110">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="b453c-111">Brama zachowa publiczny adres IP, który został z nią wcześniej powiązany.</span><span class="sxs-lookup"><span data-stu-id="b453c-111">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="b453c-112">Oznacza to, że nie będzie konieczne aktualizowanie konfiguracji routera sieci VPN pod kątem nowego publicznego adresu IP bramy sieci VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="b453c-112">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="b453c-113">Po wydaniu polecenia można zresetować bramy, natychmiast ponownego active bieżące wystąpienie bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b453c-113">When you issue the command to reset the gateway, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="b453c-114">Podczas pracy awaryjnej z aktywnym wystąpieniu (Trwa ponowne uruchamianie), do wstrzymania wystąpienia nastąpi krótką przerwę.</span><span class="sxs-lookup"><span data-stu-id="b453c-114">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="b453c-115">Przerwa powinna trwać niż dłużej niż minutę.</span><span class="sxs-lookup"><span data-stu-id="b453c-115">The gap should be less than one minute.</span></span>

<span data-ttu-id="b453c-116">Jeśli połączenie nie zostanie przywrócone po pierwszym ponownym rozruchu komputera, należy wydać to polecenie ponownie, aby uruchomić ponownie drugie wystąpienie maszyny wirtualnej (nową aktywną bramę).</span><span class="sxs-lookup"><span data-stu-id="b453c-116">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="b453c-117">Jeśli wymagane jest przeprowadzenie dwóch rozruchów jednocześnie, to ponowne uruchomienie obu wystąpień maszyn wirtualnych (aktywnego i w gotowości) będzie trwać nieco dłużej.</span><span class="sxs-lookup"><span data-stu-id="b453c-117">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="b453c-118">Spowoduje to dłuższą przerwę w łączności przez sieć VPN, trwającą maksymalnie od 2 do 4 minut, podczas której nastąpi ponowny rozruch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b453c-118">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="b453c-119">Po dwóch uruchamiany ponownie Jeśli nadal występują problemy z łącznością między różnymi lokalizacjami, otwórz żądanie obsługi z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b453c-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <span data-ttu-id="b453c-120"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b453c-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="b453c-121">Przed zresetowaniem bramy dla każdego tunelu połączenia sieci VPN typu lokacja-lokacja (site-to site, S2S) korzystającego z protokołu IPsec należy sprawdzić kluczowe elementy wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="b453c-121">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="b453c-122">Brak zgodności którychkolwiek elementów spowoduje przerwanie połączenia tuneli sieci VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="b453c-122">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="b453c-123">Sprawdzanie poprawności i usuwanie konfiguracji dla usługi lokalnej i bram sieci VPN platformy Azure pozwala uniknąć niepotrzebnych ponownych rozruchów i zakłóceń dla innych połączeń pracy w bramach.</span><span class="sxs-lookup"><span data-stu-id="b453c-123">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="b453c-124">Przed zresetowaniem bramy, sprawdź następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b453c-124">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="b453c-125">Wirtualne adresy IP (VIP) bramy sieci VPN Azure i bramy lokalnej sieci VPN powinny być prawidłowo skonfigurowane zarówno w zasadach platformy Azure, jak i zasadach lokalnej sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="b453c-125">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="b453c-126">Klucz wstępny musi być taki sam w przypadku bramy sieci VPN Azure oraz bramy lokalnej sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="b453c-126">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="b453c-127">W przypadku zastosowania konkretnej konfiguracji uwzględniającej protokół IPsec/IKE, takiej jak szyfrowanie, algorytmy wyznaczania wartości skrótu i doskonałe utajnienie przekazywania (Perfect Forward Secrecy, PFS), należy się upewnić, że zarówno brama sieci VPN Azure, jak i brama lokalnej sieci VPN mają takie same konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="b453c-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <span data-ttu-id="b453c-128"><a name="portal"></a>Azure portal</span><span class="sxs-lookup"><span data-stu-id="b453c-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="b453c-129">Można zresetować bramy sieci VPN usługi Resource Manager przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b453c-129">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="b453c-130">Jeśli chcesz zresetować klasycznego bramy, zobacz [PowerShell](#resetclassic) czynności.</span><span class="sxs-lookup"><span data-stu-id="b453c-130">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="b453c-131">Model wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b453c-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="b453c-132">Otwórz [portalu Azure](https://portal.azure.com) i przejdź do Menedżera zasobów bramy sieci wirtualnej, który chcesz zresetować.</span><span class="sxs-lookup"><span data-stu-id="b453c-132">Open the [Azure portal](https://portal.azure.com) and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="b453c-133">W bloku dla bramy sieci wirtualnej kliknij pozycję "Resetuj".</span><span class="sxs-lookup"><span data-stu-id="b453c-133">On the blade for the virtual network gateway, click 'Reset'.</span></span>

  ![Resetuj bloku bramy sieci VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="b453c-135">W bloku resetowania kliknij **zresetować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b453c-135">On the Reset blade, click the **Reset** button.</span></span>

## <span data-ttu-id="b453c-136"><a name="ps"></a>Środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="b453c-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="b453c-137">Model wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b453c-137">Resource Manager deployment model</span></span>

<span data-ttu-id="b453c-138">Polecenie cmdlet resetowania bramy jest **AzureRmVirtualNetworkGateway resetowania**.</span><span class="sxs-lookup"><span data-stu-id="b453c-138">The cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="b453c-139">Przed wykonaniem resetowanie, upewnij się, że masz najnowszą wersję [poleceń cmdlet programu PowerShell Menedżera zasobów](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="b453c-139">Before performing a reset, make sure you have the latest version of the [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="b453c-140">Poniższy przykład powoduje zresetowanie bramy sieci wirtualnej o nazwie VNet1GW w grupie zasobów TestRG1:</span><span class="sxs-lookup"><span data-stu-id="b453c-140">The following example resets a virtual network gateway named VNet1GW in the TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="b453c-141">Wynik:</span><span class="sxs-lookup"><span data-stu-id="b453c-141">Result:</span></span>

<span data-ttu-id="b453c-142">Po wyświetleniu zwracanych wyników można założyć, resetowanie bramy zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b453c-142">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="b453c-143">Jednak nie ma w wyniku zwracany, która jawnie wskazuje, że zresetowanie zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b453c-143">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="b453c-144">Jeśli chcesz należy dokładnie przejrzeć historię, aby zobaczyć dokładnie Resetowanie bramy wystąpienia, możesz wyświetlić te informacje w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b453c-144">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b453c-145">W portalu, przejdź do **"GatewayName" -> kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="b453c-145">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="b453c-146"><a name="resetclassic"></a>Klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="b453c-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="b453c-147">Polecenie cmdlet resetowania bramy jest **AzureVNetGateway resetowania**.</span><span class="sxs-lookup"><span data-stu-id="b453c-147">The cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="b453c-148">Przed wykonaniem resetowanie, upewnij się, że masz najnowszą wersję [poleceń cmdlet programu PowerShell usługi zarządzania (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="b453c-148">Before performing a reset, make sure you have the latest version of the [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="b453c-149">Poniższy przykład powoduje zresetowanie bramy sieci wirtualnej o nazwie "ContosoVNet":</span><span class="sxs-lookup"><span data-stu-id="b453c-149">The following example resets the gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="b453c-150">Wynik:</span><span class="sxs-lookup"><span data-stu-id="b453c-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="b453c-151"><a name="cli"></a>Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b453c-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="b453c-152">Aby zresetować bramy, należy użyć [zresetować bramy sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b453c-152">To reset the gateway, use the [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="b453c-153">Poniższy przykład powoduje zresetowanie bramy sieci wirtualnej o nazwie VNet5GW w grupie zasobów TestRG5:</span><span class="sxs-lookup"><span data-stu-id="b453c-153">The following example resets a virtual network gateway named VNet5GW in the TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="b453c-154">Wynik:</span><span class="sxs-lookup"><span data-stu-id="b453c-154">Result:</span></span>

<span data-ttu-id="b453c-155">Po wyświetleniu zwracanych wyników można założyć, resetowanie bramy zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b453c-155">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="b453c-156">Jednak nie ma w wyniku zwracany, która jawnie wskazuje, że zresetowanie zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b453c-156">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="b453c-157">Jeśli chcesz należy dokładnie przejrzeć historię, aby zobaczyć dokładnie Resetowanie bramy wystąpienia, możesz wyświetlić te informacje w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b453c-157">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b453c-158">W portalu, przejdź do **"GatewayName" -> kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="b453c-158">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>