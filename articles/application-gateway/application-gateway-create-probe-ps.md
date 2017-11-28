---
title: "Tworzenie niestandardowych sondowania — brama usługi aplikacji Azure — PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć niestandardowe sondowania bramy aplikacji za pomocą programu PowerShell w Menedżerze zasobów"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="7a613-103">Tworzenie niestandardowych sondowania bramy aplikacji Azure za pomocą programu PowerShell dla usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a613-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a613-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a613-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="7a613-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a613-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="7a613-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a613-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="7a613-107">W tym artykule możesz dodać niestandardowe sondowania istniejącą bramę aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a613-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="7a613-108">Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na domyślnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7a613-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="7a613-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7a613-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7a613-110">Ten artykuł dotyczy używania modelu wdrażania usługi Resource Manager zalecanego przez firmę Microsoft w przypadku większości nowych wdrożeń zamiast [klasycznego modelu wdrażania](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7a613-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="7a613-111">Utwórz bramę aplikacji z niestandardowego sondy</span><span class="sxs-lookup"><span data-stu-id="7a613-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="7a613-112">Zaloguj się i utworzyć grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="7a613-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="7a613-113">Użyj `Login-AzureRmAccount` do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7a613-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="7a613-114">Pobierz subskrypcji dla konta.</span><span class="sxs-lookup"><span data-stu-id="7a613-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="7a613-115">Wybierz subskrypcję platformy Azure do użycia.</span><span class="sxs-lookup"><span data-stu-id="7a613-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="7a613-116">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7a613-116">Create a resource group.</span></span> <span data-ttu-id="7a613-117">Ten krok można pominąć, jeśli masz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7a613-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="7a613-118">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="7a613-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7a613-119">Ta lokalizacja będzie używana jako domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7a613-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="7a613-120">Upewnij się, że wszystkie polecenia, aby utworzyć bramę aplikacji używać tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7a613-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="7a613-121">W powyższym przykładzie utworzono grupę zasobów o nazwie **zarządcy zasobów appgw** w lokalizacji **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="7a613-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="7a613-122">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="7a613-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="7a613-123">Poniższy przykład tworzy sieć wirtualną i podsieć bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="7a613-124">Brama aplikacji wymaga jego własnej podsieci do użycia.</span><span class="sxs-lookup"><span data-stu-id="7a613-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="7a613-125">Z tego powodu podsieci utworzone dla bramy aplikacji powinna być krótsza od przestrzeni adresowej sieci wirtualnej, aby umożliwić innych podsieciach utworzyć i używać.</span><span class="sxs-lookup"><span data-stu-id="7a613-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="7a613-126">Tworzenie publicznego adresu IP dla konfiguracji frontonu</span><span class="sxs-lookup"><span data-stu-id="7a613-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="7a613-127">Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **appgw-rg** dla regionu Zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="7a613-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="7a613-128">W tym przykładzie używa publicznego adresu IP dla adresu IP frontonu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="7a613-129">Brama aplikacji wymaga publiczny adres IP, w związku z tym mają nazwy DNS utworzony dynamicznie `-DomainNameLabel` nie można określić podczas tworzenia publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="7a613-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="7a613-130">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a613-130">Create an application gateway</span></span>

<span data-ttu-id="7a613-131">Wszystkie elementy konfiguracji należy zdefiniować przed utworzeniem bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="7a613-132">Poniższy przykład tworzy elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="7a613-133">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="7a613-133">**Component**</span></span> | <span data-ttu-id="7a613-134">**Opis**</span><span class="sxs-lookup"><span data-stu-id="7a613-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="7a613-135">**Konfiguracja adresu IP bramy**</span><span class="sxs-lookup"><span data-stu-id="7a613-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="7a613-136">Konfigurację adresu IP dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="7a613-137">**Puli wewnętrznej bazy danych**</span><span class="sxs-lookup"><span data-stu-id="7a613-137">**Backend pool**</span></span> | <span data-ttu-id="7a613-138">Pula adresów IP, nazw FQDN lub kart sieciowych, które są na serwery aplikacji, których hostem aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="7a613-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="7a613-139">**Badania kondycji**</span><span class="sxs-lookup"><span data-stu-id="7a613-139">**Health probe**</span></span> | <span data-ttu-id="7a613-140">Badanie niestandardowych służy do monitorowania kondycji członków puli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="7a613-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="7a613-141">**Ustawienia HTTP**</span><span class="sxs-lookup"><span data-stu-id="7a613-141">**HTTP settings**</span></span> | <span data-ttu-id="7a613-142">Kolekcja ustawień w tym, port protokołu, na podstawie plików cookie koligacji, sondy i limit czasu.</span><span class="sxs-lookup"><span data-stu-id="7a613-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="7a613-143">Te ustawienia określają, w jaki sposób ruch jest kierowany do elementów członkowskich puli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="7a613-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="7a613-144">**Port serwera sieci Web**</span><span class="sxs-lookup"><span data-stu-id="7a613-144">**Frontend port**</span></span> | <span data-ttu-id="7a613-145">Brama aplikacji w nasłuchuje ruchu na port</span><span class="sxs-lookup"><span data-stu-id="7a613-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="7a613-146">**Odbiornik**</span><span class="sxs-lookup"><span data-stu-id="7a613-146">**Listener**</span></span> | <span data-ttu-id="7a613-147">Kombinacja protokołu, konfiguracja adresu IP frontonu i port serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7a613-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="7a613-148">Jest to, co nasłuchuje przychodzących żądań.</span><span class="sxs-lookup"><span data-stu-id="7a613-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="7a613-149">**Reguły**</span><span class="sxs-lookup"><span data-stu-id="7a613-149">**Rule**</span></span>| <span data-ttu-id="7a613-150">Tras ruchu do odpowiedniej wewnętrznej bazy danych na podstawie HTTP ustawień.</span><span class="sxs-lookup"><span data-stu-id="7a613-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="7a613-151">Dodać badanie do istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a613-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="7a613-152">Poniższy fragment kodu dodaje badanie istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="7a613-153">Usuń sondę z istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a613-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="7a613-154">Poniższy fragment kodu usuwa sondę z istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="7a613-155">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="7a613-155">Get application gateway DNS name</span></span>

<span data-ttu-id="7a613-156">Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="7a613-157">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="7a613-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="7a613-158">Aby upewnić się, że użytkownicy końcowi mogą trafić bramę aplikacji, można użyć rekordu CNAME w celu wskazania publicznego punktu końcowego bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="7a613-159">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7a613-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="7a613-160">Aby to zrobić, pobierz szczegóły bramy aplikacji i skojarzony adres IP oraz nazwę DNS, używając elementu PublicIPAddress dołączonego do bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="7a613-161">Nazwa DNS bramy aplikacji powinna zostać użyta w celu utworzenia rekordu CNAME, który wskazuje dwóm aplikacjom sieci Web tę nazwę DNS.</span><span class="sxs-lookup"><span data-stu-id="7a613-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="7a613-162">Korzystanie z rekordów A nie jest zalecane, ponieważ adres VIP może ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a613-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="7a613-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a613-163">Next steps</span></span>

<span data-ttu-id="7a613-164">Dowiedz się, jak skonfigurować odciążanie protokołu SSL, przechodząc: [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="7a613-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

