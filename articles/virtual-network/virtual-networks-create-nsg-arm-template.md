---
title: "aaaCreate sieciowej grupy zabezpieczeń — szablon Menedżera zasobów Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażanie grup zabezpieczeń sieci przy użyciu szablonu usługi Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a>Tworzenie sieci za pomocą szablonu usługi Azure Resource Manager grup zabezpieczeń

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [tworzenia grup NSG w hello klasycznego modelu wdrażania](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a>Grupa NSG zasobów w pliku szablonu
Można wyświetlić i pobrać hello [przykładowy szablon](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).

Witaj w tej części opisano hello definicji hello frontonu NSG, oparte na powitania scenariusza.

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
tooassociate hello NSG toohello frontonu podsieci, masz toochange hello podsieci definicji szablonu hello i identyfikator odwołania hello Użyj hello NSG.

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

Zwróć uwagę, hello wykonywana w ramach hello zaplecza NSG hello zaplecza podsieci i w szablonie hello takie same.

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Wdrażanie szablonu ARM hello przy użyciu kliknij toodeploy
Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej. toodeploy przy użyciu tego szablonu kliknij toodeploy, postępuj zgodnie z [to łącze](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów w razie potrzeby i wykonaj te instrukcje hello hello portalu.

## <a name="deploy-hello-arm-template-by-using-powershell"></a>Wdrażanie szablonu ARM hello przy użyciu programu PowerShell
Szablon ARM hello toodeploy, który został pobrany przy użyciu programu PowerShell, wykonaj poniższe kroki hello.

1. Jeśli nie znasz programu Azure PowerShell, postępuj zgodnie z instrukcjami hello hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall i skonfigurować go.
2. Uruchom hello  **`New-AzureRmResourceGroup`**  toocreate polecenia cmdlet, grupy zasobów przy użyciu hello szablonu.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Oczekiwane dane wyjściowe:

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a>Wdrażanie szablonu ARM hello przy użyciu hello wiersza polecenia platformy Azure
Szablon ARM hello toodeploy przy użyciu hello wiersza polecenia platformy Azure, wykonaj kroki hello poniżej.

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello  **`azure config mode`**  tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.

    ```azurecli
    azure config mode arm
    ```

    Oto Hello hello oczekiwane dane wyjściowe polecenia hello:

        info:    New mode is arm

3. Uruchom hello  **`azure group deployment create`**  hello toodeploy polecenia cmdlet nowej sieci wirtualnej przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Oczekiwane dane wyjściowe:
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * **-n (lub --name)**. Nazwa toobe grupy zasobów hello utworzony.
   * **-l (lub --location)**. Region platformy Azure, w której zostanie utworzona hello grupy zasobów.
   * **-f (lub --template-file)**. Ścieżka pliku szablonu ARM tooyour.
   * **-e (lub --parameters-file)**. Ścieżka pliku parametrów ARM tooyour.

