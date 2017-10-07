---
title: aaaCreate systemu Windows maszyny Wirtualnej z szablonu na platformie Azure | Dokumentacja firmy Microsoft
description: "Szablon usługi Resource Manager i programu PowerShell tooeasily tworzenia nowej maszyny Wirtualnej systemu Windows."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Utwórz maszynę wirtualną systemu Windows z szablonem usługi Resource Manager

W tym artykule opisano sposób toodeploy usługi Azure Resource Manager szablonu przy użyciu programu PowerShell. tworzony szablon Hello wdraża jednej maszyny wirtualnej z systemem Windows Server w nowej sieci wirtualnej z pojedynczą podsiecią.

Aby uzyskać szczegółowy opis hello zasobu maszyny wirtualnej, zobacz [maszyn wirtualnych w szablonie usługi Azure Resource Manager](template-description.md). Aby uzyskać więcej informacji o wszystkich zasobów hello w szablonie, zobacz [Przewodnik po szablonie usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Należy go zająć około pięciu minut, którą toodo hello kroków w tym artykule.

## <a name="install-azure-powershell"></a>Instalowanie programu Azure PowerShell

Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](../../powershell-install-configure.md) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Wszystkie zasoby musi być wdrażana w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).

1. Pobierz listę dostępnych lokalizacji, w których można utworzyć zasoby.
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. Utwórz grupę zasobów hello w lokalizacji hello. Ten przykład przedstawia tworzenie grupy zasobów o nazwie hello **myResourceGroup** w hello **zachodnie stany USA** lokalizacji:

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a>Tworzenie plików hello

W tym kroku utworzysz plik szablonu, który wdraża hello zasobów i pliku parametrów, który dostarcza szablonu toohello wartości parametru. Możesz również utworzyć pliku autoryzacji, który jest używane tooperform operacji usługi Azure Resource Manager.

1. Utwórz plik o nazwie *CreateVMTemplate.json* i Dodaj ten tooit kodu JSON:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. Utwórz plik o nazwie *parameters.JSON następującym kodem* i Dodaj ten tooit kodu JSON:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. Utwórz nowe konto magazynu i kontener:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. Przekaż konta magazynu toohello pliki hello:

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Zmień hello — lokalizacja toohello ścieżki pliku przechowywania plików hello.

## <a name="create-hello-resources"></a>Utwórz zasoby hello

Wdrażanie szablonu hello przy użyciu parametrów hello:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> Można także wdrożyć parametry z lokalnych plików i szablonów. toolearn więcej, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Następne kroki

- Jeśli wystąpiły problemy z wdrażaniem hello, może potrwać przyjrzeć się [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
- Dowiedz się, jak toocreate i zarządzanie nimi maszynę wirtualną w [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

