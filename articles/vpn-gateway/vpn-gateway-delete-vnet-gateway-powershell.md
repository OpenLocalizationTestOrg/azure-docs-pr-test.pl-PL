---
title: "Usuwanie bramy sieci wirtualnej: środowiska PowerShell: usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Usuń bramę sieci wirtualnej przy użyciu programu PowerShell w modelu wdrażania usługi Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="bb7d2-103">Usuwanie bramy sieci wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb7d2-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb7d2-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bb7d2-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="bb7d2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb7d2-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="bb7d2-106">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="bb7d2-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="bb7d2-107">Istnieje kilka różnych metod, które można wykonać, gdy chcesz usunąć bramę sieci wirtualnej dla konfiguracji bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="bb7d2-108">Jeśli chcesz usunąć wszystkie elementy i rozpocząć od początku, tak jak w przypadku środowiska testowego, można usunąć grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="bb7d2-109">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="bb7d2-110">Jest to metoda, jest zalecane tylko jeśli nie chcesz zachować zasoby w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="bb7d2-111">Nie można selektywnie usunąć tylko kilka zasobów, przy użyciu tej metody.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="bb7d2-112">Jeśli chcesz zachować niektóre zasoby w grupie zasobów, usuwanie bramy sieci wirtualnej staje się nieco bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="bb7d2-113">Aby można było usunąć bramę sieci wirtualnej, należy najpierw usunąć wszystkie zasoby, które są zależne od bramy.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="bb7d2-114">Kroki, które należy wykonać są zależne od typu połączenia, które zostały utworzone i zasoby zależne, dla każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="bb7d2-115">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="bb7d2-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="bb7d2-116">1. Pobierz najnowsze poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="bb7d2-117">Pobierz i zainstaluj najnowszą wersję poleceń cmdlet programu PowerShell Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="bb7d2-118">Aby uzyskać więcej informacji o pobieraniu i instalowaniu poleceń cmdlet programu PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb7d2-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="bb7d2-119">2. Połącz z kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="bb7d2-120">Otwórz konsolę programu PowerShell i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="bb7d2-121">Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:</span><span class="sxs-lookup"><span data-stu-id="bb7d2-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="bb7d2-122">Sprawdź subskrypcje dostępne na koncie.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="bb7d2-123">Jeśli masz więcej niż jedną subskrypcję, określ subskrypcję, która ma być używany.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="bb7d2-124"><a name="S2S"></a>Usuwanie bramy sieci VPN typu lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="bb7d2-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="bb7d2-125">Aby usunąć bramę sieci wirtualnej S2S konfiguracji, należy najpierw usunąć wszystkie zasoby, które odnoszą się do bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="bb7d2-126">Zasoby muszą zostać usunięte w określonej kolejności z powodu zależności.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="bb7d2-127">Podczas pracy z przykłady poniżej, niektóre wartości należy określić, podczas gdy inne wartości są wynik danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="bb7d2-128">Używamy dla celów demonstracyjnych następujące wartości określonej w przykładach:</span><span class="sxs-lookup"><span data-stu-id="bb7d2-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="bb7d2-129">Nazwa sieci wirtualnej: VNet1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="bb7d2-130">Nazwa grupy zasobów: RG1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="bb7d2-131">Nazwa bramy sieci wirtualnej: GW1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="bb7d2-132">Poniższe kroki dotyczą modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="bb7d2-133">1. Pobierz bramę sieci wirtualnej, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="bb7d2-134">2. Sprawdź, czy wszystkie połączenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="bb7d2-135">3. Usuń wszystkie połączenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-135">3. Delete all connections.</span></span>

<span data-ttu-id="bb7d2-136">Może być wyświetlony monit o potwierdzenie usunięcia każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="bb7d2-137">4. Usuwanie bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="bb7d2-138">Może być wyświetlony monit o potwierdzenie usunięcia bramy.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="bb7d2-139">Jeśli masz konfigurację P2S do tej sieci wirtualnej oprócz konfiguracji S2S usuwanie bramy sieci wirtualnej automatycznie spowoduje odłączenie wszystkich klientów P2S bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="bb7d2-140">W tym momencie bramy sieci wirtualnej została usunięta.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="bb7d2-141">Następne kroki można użyć, aby usunąć wszystkie zasoby, które są już używane.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="bb7d2-142">5 usunąć bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="bb7d2-143">Pobierz listę odpowiednich bram sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="bb7d2-144">Usuwanie bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-144">Delete the local network gateways.</span></span> <span data-ttu-id="bb7d2-145">Może być wyświetlony monit o potwierdzenie usunięcia każdego z bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="bb7d2-146">6. Usuwanie zasobów adresu publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="bb7d2-147">Pobierz konfiguracje adresów IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="bb7d2-148">Pobierz listę zasobów adres publiczny adres IP używany dla tej bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="bb7d2-149">Jeśli brama sieci wirtualnej był aktywny aktywny, zostanie wyświetlony dwa publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="bb7d2-150">Usuwanie zasobów publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="bb7d2-151">7. Usuń podsieć bramy i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="bb7d2-152"><a name="v2v"></a>Usuwanie bramy sieci VPN do wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="bb7d2-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="bb7d2-153">Aby usunąć bramę sieci wirtualnej dla konfiguracji V2V, należy najpierw usunąć wszystkie zasoby, które odnoszą się do bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="bb7d2-154">Zasoby muszą zostać usunięte w określonej kolejności z powodu zależności.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="bb7d2-155">Podczas pracy z przykłady poniżej, niektóre wartości należy określić, podczas gdy inne wartości są wynik danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="bb7d2-156">Używamy dla celów demonstracyjnych następujące wartości określonej w przykładach:</span><span class="sxs-lookup"><span data-stu-id="bb7d2-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="bb7d2-157">Nazwa sieci wirtualnej: VNet1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="bb7d2-158">Nazwa grupy zasobów: RG1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="bb7d2-159">Nazwa bramy sieci wirtualnej: GW1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="bb7d2-160">Poniższe kroki dotyczą modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="bb7d2-161">1. Pobierz bramę sieci wirtualnej, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="bb7d2-162">2. Sprawdź, czy wszystkie połączenia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="bb7d2-163">Mogą istnieć inne połączenia bramy sieci wirtualnej, które są częścią innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="bb7d2-164">Sprawdź, czy dodatkowych połączeń w każdej grupie dodatkowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="bb7d2-165">W tym przykładzie firma Microsoft sprawdzanie dla połączeń z RG2.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="bb7d2-166">Uruchom to dla każdej grupy zasobów ma, które mogą mieć połączenie bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="bb7d2-167">3. Pobierz listę połączeń w obu kierunkach.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="bb7d2-168">Ponieważ jest to konfiguracja sieci wirtualnej do sieci wirtualnej, należy na liście połączeń w obu kierunkach.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="bb7d2-169">W tym przykładzie firma Microsoft sprawdzanie dla połączeń z RG2.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="bb7d2-170">Uruchom to dla każdej grupy zasobów ma, które mogą mieć połączenie bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="bb7d2-171">4. Usuń wszystkie połączenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-171">4. Delete all connections.</span></span>

<span data-ttu-id="bb7d2-172">Może być wyświetlony monit o potwierdzenie usunięcia każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="bb7d2-173">5. Usuwanie bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="bb7d2-174">Może być wyświetlony monit o potwierdzenie usunięcia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="bb7d2-175">Jeśli masz konfiguracje P2S do Twojej sieci wirtualnych oprócz konfiguracji V2V usuwanie bramy sieci wirtualnej automatycznie spowoduje odłączenie wszystkich klientów P2S bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="bb7d2-176">W tym momencie bramy sieci wirtualnej została usunięta.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="bb7d2-177">Następne kroki można użyć, aby usunąć wszystkie zasoby, które są już używane.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="bb7d2-178">6. Usuwanie zasobów adresu publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="bb7d2-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="bb7d2-179">Pobierz konfiguracje adresów IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="bb7d2-180">Pobierz listę zasobów adres publiczny adres IP używany dla tej bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="bb7d2-181">Jeśli brama sieci wirtualnej był aktywny aktywny, zostanie wyświetlony dwa publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="bb7d2-182">Usuwanie zasobów publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-182">Delete the Public IP resources.</span></span> <span data-ttu-id="bb7d2-183">Może być wyświetlony monit o potwierdzenie usunięcia publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="bb7d2-184">7. Usuń podsieć bramy i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="bb7d2-185"><a name="deletep2s"></a>Usuwanie bramy sieci VPN typu punkt-lokacja</span><span class="sxs-lookup"><span data-stu-id="bb7d2-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="bb7d2-186">Aby usunąć bramę sieci wirtualnej dla konfiguracji P2S, należy najpierw usunąć wszystkie zasoby, które odnoszą się do bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="bb7d2-187">Zasoby muszą zostać usunięte w określonej kolejności z powodu zależności.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="bb7d2-188">Podczas pracy z przykłady poniżej, niektóre wartości należy określić, podczas gdy inne wartości są wynik danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="bb7d2-189">Używamy dla celów demonstracyjnych następujące wartości określonej w przykładach:</span><span class="sxs-lookup"><span data-stu-id="bb7d2-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="bb7d2-190">Nazwa sieci wirtualnej: VNet1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="bb7d2-191">Nazwa grupy zasobów: RG1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="bb7d2-192">Nazwa bramy sieci wirtualnej: GW1</span><span class="sxs-lookup"><span data-stu-id="bb7d2-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="bb7d2-193">Poniższe kroki dotyczą modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="bb7d2-194">Po usunięciu bramy sieci VPN, wszyscy połączeni klienci zostanie odłączony od sieci wirtualnej bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="bb7d2-195">1. Pobierz bramę sieci wirtualnej, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="bb7d2-196">2. Usuwanie bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="bb7d2-197">Może być wyświetlony monit o potwierdzenie usunięcia bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="bb7d2-198">W tym momencie bramy sieci wirtualnej została usunięta.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="bb7d2-199">Następne kroki można użyć, aby usunąć wszystkie zasoby, które są już używane.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="bb7d2-200">3. Usuwanie zasobów adresu publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="bb7d2-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="bb7d2-201">Pobierz konfiguracje adresów IP bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="bb7d2-202">Pobierz listę publiczny adres IP używany dla tej bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="bb7d2-203">Jeśli brama sieci wirtualnej był aktywny aktywny, zostanie wyświetlony dwa publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="bb7d2-204">Usuń publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-204">Delete the Public IPs.</span></span> <span data-ttu-id="bb7d2-205">Może być wyświetlony monit o potwierdzenie usunięcia publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="bb7d2-206">4. Usuń podsieć bramy i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="bb7d2-207"><a name="delete"></a>Usuwanie bramy sieci VPN przez usunięcie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="bb7d2-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="bb7d2-208">Jeśli nie są dane dotyczące poszczególnych zasobów w grupie zasobów i po prostu chcesz zacząć od nowa, należy usunąć całej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="bb7d2-209">Jest to szybko Usuń całą.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="bb7d2-210">Poniższe kroki dotyczą tylko modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="bb7d2-211">1. Pobranie listy wszystkich grup zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="bb7d2-212">2. Znajdź grupę zasobów, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="bb7d2-213">Znajdź grupę zasobów, które chcesz usunąć i wyświetlanie listy zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="bb7d2-214">W tym przykładzie nazwa grupy zasobów jest RG1.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="bb7d2-215">Zmodyfikuj przykład, aby pobrać listę wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="bb7d2-216">3. Sprawdź zasoby na liście.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="bb7d2-217">Gdy lista jest zwracany, przejrzyj go, aby sprawdzić, czy chcesz usunąć wszystkie zasoby w grupie zasobów, a także samej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="bb7d2-218">Jeśli chcesz zachować niektóre zasoby w grupie zasobów, wykonaj kroki we wcześniejszych sekcjach tego artykułu można usunąć bramy.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="bb7d2-219">4. Usuń grupę zasobów i zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="bb7d2-220">Aby usunąć grupę zasobów i wszystkich zasobów znajdujących się w grupie zasobów, zmodyfikuj przykładzie i uruchom.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="bb7d2-221">5. Sprawdź stan.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-221">5. Check the status.</span></span>

<span data-ttu-id="bb7d2-222">Dopiero po pewnym czasie dla platformy Azure usunąć wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="bb7d2-223">Za pomocą tego polecenia cmdlet, można sprawdzić stan grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bb7d2-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="bb7d2-224">Wynik zwracany zawiera "Powodzenie".</span><span class="sxs-lookup"><span data-stu-id="bb7d2-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```