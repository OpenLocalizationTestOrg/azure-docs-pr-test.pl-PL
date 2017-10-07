---
title: "aaaCreate maszynę Wirtualną za pomocą statycznego publicznego adresu IP - szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązać przy użyciu szablonu usługi Azure Resource Manager toocreate maszynę Wirtualną za pomocą statycznego publicznego adresu IP."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Utwórz maszynę Wirtualną za pomocą statycznego publicznego adresu IP za pomocą szablonu usługi Azure Resource Manager

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Szablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klasyczny)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Zasoby adresów publicznych adresów IP w pliku szablonu
Można wyświetlić i pobrać hello [przykładowy szablon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Witaj w tej części opisano hello definicji hello publicznego adresu IP zasobu na podstawie scenariusza hello powyżej:

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

Powiadomienie hello **publicIPAllocationMethod** właściwość, która jest ustawiona zbyt*statycznych*. Ta właściwość może być *dynamiczne* (wartość domyślna) lub *statycznych*. Ustawienie gwarantuje toostatic, nigdy nie zmienia hello publiczny adres IP przypisany.

Witaj w tej części opisano hello skojarzenia hello publiczny adres IP z karty sieciowej:

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

Powiadomienie hello **publicznego adresu IP** Właściwość wskazująca toohello **identyfikator** zasobu o nazwie **variables('webVMSetting').pipName**. To jest nazwa hello hello publicznego adresu IP zasobu przedstawionych powyżej.

Na koniec interfejsu sieciowego hello powyżej ma na liście hello **networkProfile** właściwości hello Trwa tworzenie maszyny Wirtualnej.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Wdrażanie szablonu hello przy użyciu kliknij toodeploy

Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej. toodeploy przy użyciu tego szablonu kliknij toodeploy, kliknij przycisk **wdrażanie tooAzure** w pliku Readme.md hello hello [maszynę Wirtualną za pomocą statycznego adresu PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) szablonu. Zastąp hello domyślne wartości parametrów w razie potrzeby, a następnie wprowadź wartości parametrów puste hello.  Wykonaj instrukcje hello hello portalu toocreate maszynę wirtualną za pomocą statycznego publicznego adresu IP.

## <a name="deploy-hello-template-by-using-powershell"></a>Wdrażanie szablonu hello przy użyciu programu PowerShell

toodeploy hello szablon, który został pobrany przy użyciu programu PowerShell, wykonaj poniższe kroki hello.

1. Jeśli nie znasz programu Azure PowerShell, pełną hello etapami hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.
2. W konsoli programu PowerShell, uruchom hello `New-AzureRmResourceGroup` toocreate polecenia cmdlet nową grupę zasobów, w razie potrzeby. Jeśli masz już utworzoną grupę zasobów, przejdź toostep 3.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Oczekiwane dane wyjściowe:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. W konsoli programu PowerShell, uruchom hello `New-AzureRmResourceGroupDeployment` szablonu hello toodeploy polecenia cmdlet.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Oczekiwane dane wyjściowe:
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Wdrażanie szablonu hello przy użyciu hello wiersza polecenia platformy Azure
Szablon hello toodeploy przy użyciu hello Azure CLI, pełną hello następujące kroki:

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, wykonaj kroki hello w hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) artykuł tooinstall i skonfigurować go.
2. Uruchom hello `azure config mode` tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.

    ```azurecli
    azure config mode arm
    ```

    Witaj oczekiwane dane wyjściowe polecenia hello powyżej:

        info:    New mode is arm

3. Otwórz hello [pliku parametrów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), zaznacz zawartością i zapisz go tooa plik na swoim komputerze. Na przykład parametry hello są zapisywane tooa plik o nazwie *parameters.JSON następującym kodem*. Zmiany wartości parametrów hello w pliku hello w razie potrzeby, ale co najmniej, zaleca się zmianę wartości hello hello adminPassword parametru tooa unikatowy, złożone hasło.
4. Uruchom hello `azure group deployment create` cmd toodeploy hello nowej sieci wirtualnej przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego. W poleceniu hello poniżej, Zastąp <path> ze ścieżką hello został zapisany plik hello do. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Oczekiwane dane wyjściowe (znajduje się lista wartości parametrów używane):

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

