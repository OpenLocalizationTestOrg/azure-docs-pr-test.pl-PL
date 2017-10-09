---
title: "Resetuj tooreestablish bramy sieci VPN platformy Azure tuneli protokołu IPsec | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono zresetowanie Twojego tuneli IPsec tooreestablish bramy sieci VPN platformy Azure. Witaj artykuł dotyczy bram tooVPN w klasycznym hello i modeli wdrażania usługi Resource Manager hello."
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
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="16235-104">Resetowanie VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="16235-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="16235-105">Resetowanie bramy Azure VPN Gateway przydaje się w przypadku utraty połączenia sieci VPN obejmującego wiele lokalizacji w jednym lub wielu tunelach VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="16235-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="16235-106">W takiej sytuacji lokalnego urządzenia sieci VPN są wszystkie działa poprawnie, ale są nie jest w stanie tooestablish tuneli protokołu IPsec o hello bram sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16235-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="16235-107">Ten artykuł pomoże Ci zresetować bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="16235-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="16235-108">Co się dzieje podczas resetowania?</span><span class="sxs-lookup"><span data-stu-id="16235-108">What happens during a reset?</span></span>

<span data-ttu-id="16235-109">Brama sieci VPN składa się z dwóch wystąpień maszyn wirtualnych działających w konfiguracji aktywnego gotowości.</span><span class="sxs-lookup"><span data-stu-id="16235-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="16235-110">Zresetowanie bramy hello nastąpi ponowne uruchomienie hello bramy, a następnie ponownie stosuje hello między lokalizacjami tooit konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16235-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="16235-111">Witaj bramy przechowuje hello publicznego adresu IP, który jest już.</span><span class="sxs-lookup"><span data-stu-id="16235-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="16235-112">Oznacza to, że nie trzeba konfiguracji routera tooupdate hello sieci VPN przy użyciu nowego publicznego adresu IP dla bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16235-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="16235-113">Podczas generowania hello polecenia tooreset hello bramy natychmiast ponownego hello bieżącego aktywnego wystąpienia hello bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16235-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="16235-114">Będzie krótką przerwę w trybie failover hello z hello aktywnego wystąpienia (Trwa ponowne uruchamianie), toohello rezerwy wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="16235-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="16235-115">Odstęp Hello powinna być mniej niż minutę.</span><span class="sxs-lookup"><span data-stu-id="16235-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="16235-116">Jeśli hello połączenie nie zostało odzyskane po ponownym hello, problem sam Witaj ponownie polecenie tooreboot hello drugie wystąpienie maszyny Wirtualnej (hello nowej active bramy).</span><span class="sxs-lookup"><span data-stu-id="16235-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="16235-117">Jeśli ponownego uruchomienia hello żądanego tooback Wstecz, można nieco dłużej gdy trwa ponowne uruchamianie obu wystąpień maszyn wirtualnych (active i wstrzymania).</span><span class="sxs-lookup"><span data-stu-id="16235-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="16235-118">To spowoduje przerwę dłużej hello łączność w sieci VPN zapasowej minut too4 too2 ponowne uruchamianie hello toocomplete maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="16235-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="16235-119">Po dwóch uruchamiany ponownie Jeśli nadal występują problemy z łącznością między różnymi lokalizacjami, otwórz żądanie obsługi z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="16235-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="16235-120"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="16235-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="16235-121">Zanim je zresetujesz bramy, sprawdź hello kluczowych elementów wymienionych poniżej dla każdego tunelu VPN IPsec lokacja-lokacja (S2S).</span><span class="sxs-lookup"><span data-stu-id="16235-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="16235-122">Wszelkie niezgodność w elementach hello spowoduje rozłączenie hello tunel S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="16235-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="16235-123">Sprawdzanie poprawności i korygowanie hello konfiguracji dla usługi lokalnej i bram sieci VPN platformy Azure pozwala uniknąć niepotrzebnych ponownego uruchomienia i zakłóceń dla hello innych połączeń pracy hello bram.</span><span class="sxs-lookup"><span data-stu-id="16235-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="16235-124">Sprawdź hello poniższych elementach przed zresetowaniem bramy:</span><span class="sxs-lookup"><span data-stu-id="16235-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="16235-125">Hello Internet IP adresów (VIP) dla obu hello bramy sieci VPN platformy Azure i hello lokalnej bramy sieci VPN są poprawnie skonfigurowane w obu hello Azure i hello lokalnej sieci VPN zasad.</span><span class="sxs-lookup"><span data-stu-id="16235-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="16235-126">klucz wstępny Hello musi hello w tej samej na bramy sieci VPN platformy Azure, jak i dla lokalnego.</span><span class="sxs-lookup"><span data-stu-id="16235-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="16235-127">W przypadku zastosowania określonej konfiguracji protokołu IPsec/IKE, takie jak szyfrowania, mieszania algorytmów i doskonałego utajnienia przekazywania (Perfect Forward Secrecy), upewnij się, zarówno hello Azure i lokalnymi bramy sieci VPN mają hello takie same konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="16235-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="16235-128"><a name="portal"></a>Azure portal</span><span class="sxs-lookup"><span data-stu-id="16235-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="16235-129">Można zresetować bramy VPN Resource Manager przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="16235-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="16235-130">Jeśli tooreset klasycznego bramy, zobacz hello [PowerShell](#resetclassic) czynności.</span><span class="sxs-lookup"><span data-stu-id="16235-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="16235-131">Model wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="16235-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="16235-132">Otwórz hello [portalu Azure](https://portal.azure.com) i przejdź toohello bramy sieci wirtualnej dla Menedżera zasobów, które mają tooreset.</span><span class="sxs-lookup"><span data-stu-id="16235-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="16235-133">W bloku hello hello bramy sieci wirtualnej kliknij pozycję "Resetuj".</span><span class="sxs-lookup"><span data-stu-id="16235-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![Resetuj bloku bramy sieci VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="16235-135">Na powitania resetowania bloku, kliknij hello **zresetować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="16235-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="16235-136"><a name="ps"></a>Środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="16235-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="16235-137">Model wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="16235-137">Resource Manager deployment model</span></span>

<span data-ttu-id="16235-138">Witaj polecenia cmdlet Resetowanie bramy jest **AzureRmVirtualNetworkGateway resetowania**.</span><span class="sxs-lookup"><span data-stu-id="16235-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="16235-139">Przed wykonaniem resetowanie, upewnij się, że masz najnowszą wersję hello hello [poleceń cmdlet programu PowerShell Menedżera zasobów](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="16235-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="16235-140">Witaj poniższy przykład powoduje zresetowanie bramy sieci wirtualnej o nazwie VNet1GW w grupie zasobów TestRG1 hello:</span><span class="sxs-lookup"><span data-stu-id="16235-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="16235-141">Wynik:</span><span class="sxs-lookup"><span data-stu-id="16235-141">Result:</span></span>

<span data-ttu-id="16235-142">Po wyświetleniu zwracanych wyników można założyć, resetowanie bramy hello zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="16235-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="16235-143">Jednak nie ma w wyniku zwracany hello, która jawnie wskazuje, że resetowania hello zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="16235-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="16235-144">Jeśli chcesz, aby toolook ściśle na powitania historii toosee dokładnie bramy hello zresetowanie wystąpił, można wyświetlić te informacje w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16235-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="16235-145">W portalu hello Przejdź zbyt**"GatewayName" -> kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="16235-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="16235-146"><a name="resetclassic"></a>Klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="16235-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="16235-147">Witaj polecenia cmdlet Resetowanie bramy jest **AzureVNetGateway resetowania**.</span><span class="sxs-lookup"><span data-stu-id="16235-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="16235-148">Przed wykonaniem resetowanie, upewnij się, że masz najnowszą wersję hello hello [poleceń cmdlet programu PowerShell usługi zarządzania (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="16235-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="16235-149">Witaj poniższy przykład resetuje hello bramy sieci wirtualnej o nazwie "ContosoVNet":</span><span class="sxs-lookup"><span data-stu-id="16235-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="16235-150">Wynik:</span><span class="sxs-lookup"><span data-stu-id="16235-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="16235-151"><a name="cli"></a>Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="16235-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="16235-152">tooreset hello bramy, użyj hello [zresetować bramy sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) polecenia.</span><span class="sxs-lookup"><span data-stu-id="16235-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="16235-153">Witaj poniższy przykład powoduje zresetowanie bramy sieci wirtualnej o nazwie VNet5GW w grupie zasobów TestRG5 hello:</span><span class="sxs-lookup"><span data-stu-id="16235-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="16235-154">Wynik:</span><span class="sxs-lookup"><span data-stu-id="16235-154">Result:</span></span>

<span data-ttu-id="16235-155">Po wyświetleniu zwracanych wyników można założyć, resetowanie bramy hello zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="16235-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="16235-156">Jednak nie ma w wyniku zwracany hello, która jawnie wskazuje, że resetowania hello zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="16235-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="16235-157">Jeśli chcesz, aby toolook ściśle na powitania historii toosee dokładnie bramy hello zresetowanie wystąpił, można wyświetlić te informacje w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16235-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="16235-158">W portalu hello Przejdź zbyt**"GatewayName" -> kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="16235-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
