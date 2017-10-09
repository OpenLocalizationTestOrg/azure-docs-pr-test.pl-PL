---
title: "aaaCreate niestandardowego sondowania — brama usługi aplikacji Azure — PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate niestandardowego sondowania bramy aplikacji za pomocą programu PowerShell w programie Menedżer zasobów"
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
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="7b0e3-103">Tworzenie niestandardowych sondowania bramy aplikacji Azure za pomocą programu PowerShell dla usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b0e3-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b0e3-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b0e3-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="7b0e3-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b0e3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="7b0e3-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b0e3-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="7b0e3-107">W tym artykule możesz dodać niestandardowe sondowania tooan istniejących aplikacji bramy przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="7b0e3-108">Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na powitania domyślnej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="7b0e3-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7b0e3-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7b0e3-110">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7b0e3-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="7b0e3-111">Utwórz bramę aplikacji z niestandardowego sondy</span><span class="sxs-lookup"><span data-stu-id="7b0e3-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="7b0e3-112">Zaloguj się i utworzyć grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="7b0e3-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="7b0e3-113">Użyj `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="7b0e3-114">Pobierz subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="7b0e3-115">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="7b0e3-116">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-116">Create a resource group.</span></span> <span data-ttu-id="7b0e3-117">Ten krok można pominąć, jeśli masz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="7b0e3-118">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7b0e3-119">Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="7b0e3-120">Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="7b0e3-121">W hello poprzedzających przykład, utworzyliśmy grupę zasobów o nazwie **zarządcy zasobów appgw** w lokalizacji **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="7b0e3-122">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="7b0e3-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="7b0e3-123">Witaj poniższy przykład tworzy sieć wirtualną i podsieć bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="7b0e3-124">Brama aplikacji wymaga jego własnej podsieci do użycia.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="7b0e3-125">Z tego powodu podsieci hello utworzone dla bramy aplikacji hello powinna być krótsza od przestrzeni adresowej hello hello tooallow sieci Wirtualnej dla innych toobe podsieci tworzone i używane.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="7b0e3-126">Utwórz publiczny adres IP dla konfiguracji frontonu hello</span><span class="sxs-lookup"><span data-stu-id="7b0e3-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="7b0e3-127">Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="7b0e3-128">W tym przykładzie używa publicznego adresu IP hello adres IP frontonu bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="7b0e3-129">Brama aplikacji wymaga hello publicznego adresu IP adres toohave utworzony dynamicznie nazwy DNS w związku z tym hello `-DomainNameLabel` nie można określić podczas tworzenia hello hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="7b0e3-130">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="7b0e3-130">Create an application gateway</span></span>

<span data-ttu-id="7b0e3-131">Przed utworzeniem bramy aplikacji hello skonfigurować wszystkich elementów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="7b0e3-132">Witaj poniższy przykład tworzy hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="7b0e3-133">**Składnik**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-133">**Component**</span></span> | <span data-ttu-id="7b0e3-134">**Opis**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="7b0e3-135">**Konfiguracja adresu IP bramy**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="7b0e3-136">Konfigurację adresu IP dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="7b0e3-137">**Puli wewnętrznej bazy danych**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-137">**Backend pool**</span></span> | <span data-ttu-id="7b0e3-138">Pula adresów IP, nazw FQDN lub kart sieciowych, które są serwerami aplikacji toohello, które zawierają hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="7b0e3-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="7b0e3-139">**Badania kondycji**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-139">**Health probe**</span></span> | <span data-ttu-id="7b0e3-140">Niestandardowe sondowania używany kondycji hello toomonitor elementów członkowskich puli zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="7b0e3-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="7b0e3-141">**Ustawienia HTTP**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-141">**HTTP settings**</span></span> | <span data-ttu-id="7b0e3-142">Kolekcja ustawień w tym, port protokołu, na podstawie plików cookie koligacji, sondy i limit czasu.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="7b0e3-143">Te ustawienia określają, jaki ruch jest członków puli zaplecza toohello routingiem</span><span class="sxs-lookup"><span data-stu-id="7b0e3-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="7b0e3-144">**Port serwera sieci Web**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-144">**Frontend port**</span></span> | <span data-ttu-id="7b0e3-145">port Hello bramy aplikacji hello nasłuchuje ruchu na</span><span class="sxs-lookup"><span data-stu-id="7b0e3-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="7b0e3-146">**Odbiornik**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-146">**Listener**</span></span> | <span data-ttu-id="7b0e3-147">Kombinacja protokołu, konfiguracja adresu IP frontonu i port serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="7b0e3-148">Jest to, co nasłuchuje przychodzących żądań.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="7b0e3-149">**Reguły**</span><span class="sxs-lookup"><span data-stu-id="7b0e3-149">**Rule**</span></span>| <span data-ttu-id="7b0e3-150">Trasy hello ruchu toohello odpowiedniej wewnętrznej bazy danych na podstawie ustawień protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="7b0e3-151">Dodaj bramę sondowania tooan istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="7b0e3-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="7b0e3-152">Witaj poniższy fragment kodu dodaje sondowania tooan istniejących aplikacji bramę.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="7b0e3-153">Usuń sondę z istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="7b0e3-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="7b0e3-154">Witaj następującego fragmentu kodu usuwa sondę z istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="7b0e3-155">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="7b0e3-155">Get application gateway DNS name</span></span>

<span data-ttu-id="7b0e3-156">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="7b0e3-157">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="7b0e3-158">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello rekord CNAME może służyć toopoint toohello publiczny punkt końcowy hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="7b0e3-159">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b0e3-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="7b0e3-160">toodo tego pobierania szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="7b0e3-161">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="7b0e3-162">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b0e3-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7b0e3-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b0e3-163">Next steps</span></span>

<span data-ttu-id="7b0e3-164">Dowiedz się tooconfigure odciążanie protokołu SSL, przechodząc: [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="7b0e3-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

