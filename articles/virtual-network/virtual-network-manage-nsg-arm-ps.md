---
title: "aaaManage sieciowej grupy zabezpieczeń - programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage sieciowych grup zabezpieczeń za pomocą programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>Zarządzanie grupami zabezpieczeń sieci przy użyciu programu PowerShell

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>Pobieranie informacji
Można wyświetlić istniejących grup NSG, pobrać reguł dla istniejącej grupy NSG i dowiedzieć się, jakie zasoby grupy NSG jest skojarzona z.

### <a name="view-existing-nsgs"></a>Wyświetlanie istniejących grup NSG
tooview wszystkich istniejących grup NSG w ramach subskrypcji, uruchom hello `Get-AzureRmNetworkSecurityGroup` polecenia cmdlet.

Oczekiwany wynik:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


tooview hello lista grup NSG w określonej grupy zasobów, uruchom hello `Get-AzureRmNetworkSecurityGroup` polecenia cmdlet.

Oczekiwane dane wyjściowe:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>Wyświetl listę wszystkich reguł dla grupy NSG
tooview hello reguły NSG o nazwie **frontonu NSG**, wprowadź następujące polecenie hello:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

Oczekiwane dane wyjściowe:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> Można również użyć `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello domyślnych reguł z hello **frontonu NSG** NSG.
> 

### <a name="view-nsgs-associations"></a>Wyświetlanie grup NSG powiązań
tooview hello jakie zasoby **frontonu NSG** grupa NSG jest Skojarz z, uruchom hello następujące polecenie:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Wyszukaj hello **Networkinterface** i **podsieci** właściwości, jak pokazano poniżej:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

W poprzednim przykładzie hello hello NSG nie jest skojarzony tooany interfejsów sieciowych (NIC); jest tooa skojarzonych podsieci o nazwie **frontonu**.

## <a name="manage-rules"></a>Zarządzaj regułami
Można dodawać reguły tooan istniejące grupy NSG, edytować istniejące zasady i Usuń reguły.

### <a name="add-a-rule"></a>Dodawanie reguły
tooadd, dzięki czemu reguły **przychodzących** tooport ruchu **443** z dowolnej maszyny toohello **NSG frontonu** NSG, pełną hello następujące kroki:

1. Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Uruchom następujące polecenie tooadd hello toohello reguły NSG:

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello zmian toohello NSG, uruchom następujące polecenie hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    Oczekiwane dane wyjściowe, pokazujący tylko hello reguły zabezpieczeń:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>Zmień reguły
Reguła hello toochange utworzone powyżej tooallow ruchu przychodzącego ruchu z hello **Internet** , wykonaj poniższe kroki hello.

1. Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Uruchom następujące polecenie, używając nowego ustawienia reguły hello hello:

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello zmian toohello NSG, uruchom następujące polecenie hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Oczekiwane dane wyjściowe, pokazujący tylko hello reguły zabezpieczeń:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>Usuwanie reguły
1. Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hello uruchom następujące polecenie tooremove hello reguły hello NSG:

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Zapisz toohello zmian hello NSG, uruchamiając następujące polecenie hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Oczekiwane dane wyjściowe, pokazujący tylko hello reguły zabezpieczeń, powiadomienia hello **reguła https** nie jest już wyświetlane:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>Zarządzanie skojarzenia
Możesz skojarzyć toosubnets NSG i kart interfejsu sieciowego. Można również usunąć skojarzenie grupy NSG z dowolnego zasobu, który jest ona skojarzona.

### <a name="associate-an-nsg-tooa-nic"></a>Kojarzenie grupy NSG tooa karty Sieciowej
Witaj tooassociate **frontonu NSG** NSG toohello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:

1. Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hello uruchom następujące polecenie hello tooretrieve istniejących kart interfejsu Sieciowego i zapisze go w zmiennej:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **kart** wartość zmiennej toohello hello **NSG** zmiennej, wprowadzając następujące polecenie hello:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. toosave hello zmian toohello karty Sieciowej, uruchom następujące polecenie hello:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Oczekiwane dane wyjściowe przedstawiający tylko hello **grupy NetworkSecurityGroup** właściwości:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>Usuń skojarzenie grupy NSG z karty Sieciowej
Witaj toodissociate **frontonu NSG** grupy NSG z hello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:

1. Hello uruchom następujące polecenie hello tooretrieve istniejących kart interfejsu Sieciowego i zapisze go w zmiennej:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **kart** zmiennej zbyt**$null** , uruchamiając następujące polecenie hello:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. toosave hello zmian toohello karty Sieciowej, uruchom następujące polecenie hello:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Oczekiwane dane wyjściowe przedstawiający tylko hello **grupy NetworkSecurityGroup** właściwości:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>Usuń skojarzenie grupy NSG z podsiecią
Witaj toodissociate **frontonu NSG** grupy NSG z hello **frontonu** podsieci, pełną hello następujące kroki:

1. Hello uruchom następujące polecenie hello tooretrieve istniejącej sieci wirtualnej i zapisze go w zmiennej:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Uruchom hello następujące polecenia tooretrieve hello **frontonu** podsieci i zapisze go w zmiennej:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **podsieci** zmiennej zbyt**$null** wprowadzając hello następujące polecenie:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. toosave hello zmian toohello podsieci, uruchom następujące polecenie hello:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Oczekiwane dane wyjściowe wyświetlane tylko hello właściwości hello **frontonu** podsieci. Powiadomienie nie ma właściwości **grupy NetworkSecurityGroup**:
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>Kojarzenie grupy NSG podsieci tooa
Witaj tooassociate **frontonu NSG** NSG toohello **FronEnd** ponownie podsieci, pełną hello następujące kroki:

1. Hello uruchom następujące polecenie hello tooretrieve istniejącej sieci wirtualnej i zapisze go w zmiennej:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Uruchom hello następujące polecenia tooretrieve hello **frontonu** podsieci i zapisze go w zmiennej:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **podsieci** zmiennej zbyt**$null** , uruchamiając następujące polecenie hello:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. toosave hello zmian toohello podsieci, uruchom następujące polecenie hello:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Oczekiwane dane wyjściowe przedstawiający tylko hello **grupy NetworkSecurityGroup** właściwości hello **frontonu** podsieci:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>Usuwanie grupy NSG
Grupy NSG można usuwać tylko, jeśli nie został skojarzony tooany zasobów. toodelete grupy NSG, wykonaj poniższe kroki hello.

1. zasoby hello toocheck skojarzony tooan NSG, uruchom hello `azure network nsg show` pokazane [skojarzenia grup NSG widoku](#View-NSGs-associations).
2. Jeśli hello grupa NSG jest skojarzona tooany kart sieciowych, uruchom hello `azure network nic set` pokazane [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC) dla poszczególnych kart sieciowych. 
3. Jeśli hello NSG jest skojarzona tooany podsieci, uruchom hello `azure network vnet subnet set` pokazane [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet) dla każdej podsieci.
4. Uruchom następujące polecenie hello hello toodelete NSG:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > Witaj `-Force` parametru zapewnia nie ma potrzeby usuwania hello tooconfirm.
   > 

## <a name="next-steps"></a>Następne kroki
* [Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.

