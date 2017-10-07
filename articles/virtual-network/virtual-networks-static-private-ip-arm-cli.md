---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych za pomocą hello Azure interfejsu wiersza polecenia (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej z wykorzystaniem hello Azure CLI 2.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia 

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia: 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [Zarządzanie statycznego prywatnego adresu IP w hello klasycznego modelu wdrażania](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> Poniższe polecenia Azure CLI 2.0 próbki Hello oczekiwać środowisku niezłożonym już utworzone. Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe hello opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Określanie statycznego prywatnego adresu IP podczas tworzenia maszyny Wirtualnej

toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet* z statycznego prywatnego adresu IP z *192.168.1.101*, Wykonaj poniższe kroki hello:

1. Jeśli nie zostało jeszcze, instalowania i konfigurowania hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login). 

2. Utwórz publiczny adres IP dla hello maszyny Wirtualnej z hello [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create) polecenia. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.

    > [!NOTE]
    > Może dokonać lub wymagane toouse różne wartości dla argumentów w tej i kolejnych krokach, w zależności od środowiska.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Oczekiwane dane wyjściowe:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Nazwa grupy zasobów hello, w których toocreate hello publicznego adresu IP.
   * `--name`: Nazwa hello publicznego adresu IP.
   * `--location`: Region platformy azure, w których toocreate hello publicznego adresu IP.

3. Uruchom hello [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create) toocreate polecenia ze statycznego prywatnego adresu IP karty Sieciowej. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Oczekiwane dane wyjściowe:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Parametry:

    * `--private-ip-address`: Statycznego prywatnego adresu IP dla hello karty sieciowej.
    * `--vnet-name`: Name hello sieci wirtualnej, w których toocreate hello karty sieciowej.
    * `--subnet`: Name hello podsieci, w których hello toocreate karty sieciowej.

4. Uruchom hello [tworzenia maszyny wirtualnej azure](/cli/azure/vm/nic#create) hello toocreate polecenia przy użyciu hello publicznego adresu IP i karty Sieciowej maszyny Wirtualnej utworzone powyżej. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Oczekiwane dane wyjściowe:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Parametrów innych niż podstawowe hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) parametrów.

   * `--nics`: Nazwa hello kart toowhich hello maszyny Wirtualnej jest dołączony.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Pobrać statycznych prywatne informacje o adresie IP dla maszyny Wirtualnej

tooview hello statycznego prywatnego adresu IP, który został utworzony, uruchom następujące polecenie z wiersza polecenia platformy Azure hello i sprawdź wartości hello *metody alokacji prywatnego adresu IP* i *prywatny adres IP*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Oczekiwane dane wyjściowe:

```json
"192.168.1.101"
```

toodisplay hello określone informacje IP hello karty Sieciowej dla tej maszyny Wirtualnej, zapytania hello karty Sieciowej, w szczególności:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

dane wyjściowe Hello to wyglądać mniej więcej tak:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Usuń statycznego prywatnego adresu IP z maszyny Wirtualnej

Nie można usunąć statycznego prywatnego adresu IP z karty Sieciowej w wiersza polecenia platformy Azure dla wdrożenia Menedżera zasobów. Należy:
- Utwórz nowy kartę Sieciową, która korzysta z dynamicznego adresu IP
- Hello karty Sieciowej na powitania hello maszyny Wirtualnej nowo utworzony zestaw kart sieciowych. 

toochange hello kart interfejsu Sieciowego dla powitalne wirtualna używana w hello poleceń powyżej, wykonaj kroki hello poniżej.

1. Uruchom hello **tworzenie kart interfejsu sieciowego azure** polecenia toocreate nowej karty Sieciowej, za pomocą alokacji dynamicznego adresu IP za pomocą nowego adresu IP. Należy pamiętać, że żaden adres IP, ponieważ określono metodę alokacji hello **dynamiczne**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Oczekiwane dane wyjściowe:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Uruchom hello **zestawu azure vm** hello toochange polecenia używane przez hello maszyny Wirtualnej karty Sieciowej.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Oczekiwane dane wyjściowe:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Jeśli hello maszyna wirtualna jest wystarczająco duży toohave więcej niż jedną kartę Sieciową, uruchom hello **usunąć kart interfejsu sieciowego azure** polecenia toodelete hello starego karty sieciowej.
   
## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.
* Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.
* Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).

