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
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="d5a83-103">Utwórz maszynę wirtualną systemu Windows z szablonem usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5a83-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="d5a83-104">W tym artykule opisano sposób toodeploy usługi Azure Resource Manager szablonu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5a83-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="d5a83-105">tworzony szablon Hello wdraża jednej maszyny wirtualnej z systemem Windows Server w nowej sieci wirtualnej z pojedynczą podsiecią.</span><span class="sxs-lookup"><span data-stu-id="d5a83-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="d5a83-106">Aby uzyskać szczegółowy opis hello zasobu maszyny wirtualnej, zobacz [maszyn wirtualnych w szablonie usługi Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="d5a83-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="d5a83-107">Aby uzyskać więcej informacji o wszystkich zasobów hello w szablonie, zobacz [Przewodnik po szablonie usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d5a83-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="d5a83-108">Należy go zająć około pięciu minut, którą toodo hello kroków w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="d5a83-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="d5a83-109">Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5a83-109">Install Azure PowerShell</span></span>

<span data-ttu-id="d5a83-110">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](../../powershell-install-configure.md) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="d5a83-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="d5a83-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d5a83-111">Create a resource group</span></span>

<span data-ttu-id="d5a83-112">Wszystkie zasoby musi być wdrażana w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5a83-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="d5a83-113">Pobierz listę dostępnych lokalizacji, w których można utworzyć zasoby.</span><span class="sxs-lookup"><span data-stu-id="d5a83-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="d5a83-114">Utwórz grupę zasobów hello w lokalizacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5a83-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="d5a83-115">Ten przykład przedstawia tworzenie grupy zasobów o nazwie hello **myResourceGroup** w hello **zachodnie stany USA** lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="d5a83-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="d5a83-116">Tworzenie plików hello</span><span class="sxs-lookup"><span data-stu-id="d5a83-116">Create hello files</span></span>

<span data-ttu-id="d5a83-117">W tym kroku utworzysz plik szablonu, który wdraża hello zasobów i pliku parametrów, który dostarcza szablonu toohello wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="d5a83-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="d5a83-118">Możesz również utworzyć pliku autoryzacji, który jest używane tooperform operacji usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d5a83-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="d5a83-119">Utwórz plik o nazwie *CreateVMTemplate.json* i Dodaj ten tooit kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="d5a83-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

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

2. <span data-ttu-id="d5a83-120">Utwórz plik o nazwie *parameters.JSON następującym kodem* i Dodaj ten tooit kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="d5a83-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

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

3. <span data-ttu-id="d5a83-121">Utwórz nowe konto magazynu i kontener:</span><span class="sxs-lookup"><span data-stu-id="d5a83-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="d5a83-122">Przekaż konta magazynu toohello pliki hello:</span><span class="sxs-lookup"><span data-stu-id="d5a83-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="d5a83-123">Zmień hello — lokalizacja toohello ścieżki pliku przechowywania plików hello.</span><span class="sxs-lookup"><span data-stu-id="d5a83-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="d5a83-124">Utwórz zasoby hello</span><span class="sxs-lookup"><span data-stu-id="d5a83-124">Create hello resources</span></span>

<span data-ttu-id="d5a83-125">Wdrażanie szablonu hello przy użyciu parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="d5a83-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="d5a83-126">Można także wdrożyć parametry z lokalnych plików i szablonów.</span><span class="sxs-lookup"><span data-stu-id="d5a83-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="d5a83-127">toolearn więcej, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="d5a83-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5a83-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5a83-128">Next Steps</span></span>

- <span data-ttu-id="d5a83-129">Jeśli wystąpiły problemy z wdrażaniem hello, może potrwać przyjrzeć się [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="d5a83-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="d5a83-130">Dowiedz się, jak toocreate i zarządzanie nimi maszynę wirtualną w [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5a83-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

