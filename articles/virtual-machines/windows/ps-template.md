---
title: Tworzenie maszyny Wirtualnej systemu Windows z szablonu na platformie Azure | Dokumentacja firmy Microsoft
description: "Łatwe tworzenie nowej maszyny Wirtualnej systemu Windows przy użyciu szablonu usługi Resource Manager i programu PowerShell."
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
ms.openlocfilehash: ddab80262fe27c1f5995858ec7de75d7c46df081
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="b70d0-103">Utwórz maszynę wirtualną systemu Windows z szablonem usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b70d0-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="b70d0-104">W tym artykule przedstawiono sposób wdrażania szablonu usługi Azure Resource Manager przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b70d0-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="b70d0-105">Tworzony szablon wdraża jednej maszyny wirtualnej z systemem Windows Server w nowej sieci wirtualnej z pojedynczą podsiecią.</span><span class="sxs-lookup"><span data-stu-id="b70d0-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="b70d0-106">Aby uzyskać szczegółowy opis zasobu maszyny wirtualnej, zobacz [maszyn wirtualnych w szablonie usługi Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="b70d0-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="b70d0-107">Aby uzyskać więcej informacji na temat wszystkich zasobów w szablonie, zobacz [Przewodnik po szablonie usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="b70d0-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="b70d0-108">Wykonaj kroki opisane w tym artykule powinno zająć około pięciu minut.</span><span class="sxs-lookup"><span data-stu-id="b70d0-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="b70d0-109">Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b70d0-109">Install Azure PowerShell</span></span>

<span data-ttu-id="b70d0-110">Zobacz [How to install and configure Azure PowerShell](../../powershell-install-configure.md) (Jak zainstalować i skonfigurować program Azure PowerShell), aby uzyskać informacje na temat instalowania najnowszej wersji programu Azure PowerShell, wybierania subskrypcji i logowania się do konta.</span><span class="sxs-lookup"><span data-stu-id="b70d0-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="b70d0-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="b70d0-111">Create a resource group</span></span>

<span data-ttu-id="b70d0-112">Wszystkie zasoby musi być wdrażana w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b70d0-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="b70d0-113">Pobierz listę dostępnych lokalizacji, w których można utworzyć zasoby.</span><span class="sxs-lookup"><span data-stu-id="b70d0-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="b70d0-114">Utwórz grupę zasobów w wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b70d0-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="b70d0-115">Ten przykład przedstawia tworzenie grupy zasobów o nazwie **myResourceGroup** w **zachodnie stany USA** lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="b70d0-115">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="b70d0-116">Tworzenie plików</span><span class="sxs-lookup"><span data-stu-id="b70d0-116">Create the files</span></span>

<span data-ttu-id="b70d0-117">W tym kroku utworzysz pliku szablonu, który wdraża zasobów i pliku parametrów, które dostarcza wartości parametru do szablonu.</span><span class="sxs-lookup"><span data-stu-id="b70d0-117">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="b70d0-118">Możesz również utworzyć pliku autoryzacji, który służy do wykonywania operacji usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b70d0-118">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="b70d0-119">Utwórz plik o nazwie *CreateVMTemplate.json* i Dodaj ten kod JSON do niej:</span><span class="sxs-lookup"><span data-stu-id="b70d0-119">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

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

2. <span data-ttu-id="b70d0-120">Utwórz plik o nazwie *parameters.JSON następującym kodem* i Dodaj ten kod JSON do niej:</span><span class="sxs-lookup"><span data-stu-id="b70d0-120">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

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

3. <span data-ttu-id="b70d0-121">Utwórz nowe konto magazynu i kontener:</span><span class="sxs-lookup"><span data-stu-id="b70d0-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="b70d0-122">Przekazywanie plików do konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="b70d0-122">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="b70d0-123">Zmiana - ścieżki do plików do lokalizacji, w którym są przechowywane pliki.</span><span class="sxs-lookup"><span data-stu-id="b70d0-123">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="b70d0-124">Utworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="b70d0-124">Create the resources</span></span>

<span data-ttu-id="b70d0-125">Wdrażanie szablonu przy użyciu parametrów:</span><span class="sxs-lookup"><span data-stu-id="b70d0-125">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="b70d0-126">Można także wdrożyć parametry z lokalnych plików i szablonów.</span><span class="sxs-lookup"><span data-stu-id="b70d0-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="b70d0-127">Aby dowiedzieć się więcej, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="b70d0-127">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b70d0-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b70d0-128">Next Steps</span></span>

- <span data-ttu-id="b70d0-129">Jeśli wystąpiły problemy dotyczące wdrożenia, może potrwać przyjrzeć się [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b70d0-129">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="b70d0-130">Informacje o sposobie tworzenia i zarządzania nimi maszynę wirtualną w [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b70d0-130">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

