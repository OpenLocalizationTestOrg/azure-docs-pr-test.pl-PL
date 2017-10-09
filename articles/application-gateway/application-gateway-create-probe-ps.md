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
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a>Tworzenie niestandardowych sondowania bramy aplikacji Azure za pomocą programu PowerShell dla usługi Azure Resource Manager

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-probe-ps.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-probe-classic-ps.md)

W tym artykule możesz dodać niestandardowe sondowania tooan istniejących aplikacji bramy przy użyciu programu PowerShell. Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na powitania domyślnej aplikacji sieci web.

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](application-gateway-create-probe-classic-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a>Utwórz bramę aplikacji z niestandardowego sondy

### <a name="sign-in-and-create-resource-group"></a>Zaloguj się i utworzyć grupę zasobów

1. Użyj `Login-AzureRmAccount` tooauthenticate.

  ```powershell
  Login-AzureRmAccount
  ```

1. Pobierz subskrypcje hello hello konta.

  ```powershell
  Get-AzureRmSubscription
  ```

1. Wybierz z toouse Twojej subskrypcji platformy Azure.

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. Utwórz grupę zasobów. Ten krok można pominąć, jeśli masz istniejącą grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.

W hello poprzedzających przykład, utworzyliśmy grupę zasobów o nazwie **zarządcy zasobów appgw** w lokalizacji **zachodnie stany USA**.

### <a name="create-a-virtual-network-and-a-subnet"></a>Tworzenie sieci wirtualnej i podsieci

Witaj poniższy przykład tworzy sieć wirtualną i podsieć bramy aplikacji hello. Brama aplikacji wymaga jego własnej podsieci do użycia. Z tego powodu podsieci hello utworzone dla bramy aplikacji hello powinna być krótsza od przestrzeni adresowej hello hello tooallow sieci Wirtualnej dla innych toobe podsieci tworzone i używane.

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Utwórz publiczny adres IP dla konfiguracji frontonu hello

Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA. W tym przykładzie używa publicznego adresu IP hello adres IP frontonu bramy aplikacji hello.  Brama aplikacji wymaga hello publicznego adresu IP adres toohave utworzony dynamicznie nazwy DNS w związku z tym hello `-DomainNameLabel` nie można określić podczas tworzenia hello hello publicznego adresu IP.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

Przed utworzeniem bramy aplikacji hello skonfigurować wszystkich elementów konfiguracji. Witaj poniższy przykład tworzy hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.

| **Składnik** | **Opis** |
|---|---|
| **Konfiguracja adresu IP bramy** | Konfigurację adresu IP dla bramy aplikacji.|
| **Puli wewnętrznej bazy danych** | Pula adresów IP, nazw FQDN lub kart sieciowych, które są serwerami aplikacji toohello, które zawierają hello aplikacji sieci web|
| **Badania kondycji** | Niestandardowe sondowania używany kondycji hello toomonitor elementów członkowskich puli zaplecza hello|
| **Ustawienia HTTP** | Kolekcja ustawień w tym, port protokołu, na podstawie plików cookie koligacji, sondy i limit czasu.  Te ustawienia określają, jaki ruch jest członków puli zaplecza toohello routingiem|
| **Port serwera sieci Web** | port Hello bramy aplikacji hello nasłuchuje ruchu na|
| **Odbiornik** | Kombinacja protokołu, konfiguracja adresu IP frontonu i port serwera sieci Web. Jest to, co nasłuchuje przychodzących żądań.
|**Reguły**| Trasy hello ruchu toohello odpowiedniej wewnętrznej bazy danych na podstawie ustawień protokołu HTTP.|

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

## <a name="add-a-probe-tooan-existing-application-gateway"></a>Dodaj bramę sondowania tooan istniejącej aplikacji

Witaj poniższy fragment kodu dodaje sondowania tooan istniejących aplikacji bramę.

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

## <a name="remove-a-probe-from-an-existing-application-gateway"></a>Usuń sondę z istniejącą bramę aplikacji

Witaj następującego fragmentu kodu usuwa sondę z istniejącą bramę aplikacji.

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

## <a name="get-application-gateway-dns-name"></a>Pobieranie nazwy DNS bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna. Użytkownicy końcowi tooensure można trafień bramy aplikacji hello rekord CNAME może służyć toopoint toohello publiczny punkt końcowy hello bramy aplikacji. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo tego pobierania szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone. Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.

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

## <a name="next-steps"></a>Następne kroki

Dowiedz się tooconfigure odciążanie protokołu SSL, przechodząc: [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)

