---
title: "Kontrolowanie routingu i wirtualnych urządzeń w usłudze Azure - szablonu | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie kontrolowania routingu i wirtualnych urządzeń przy użyciu szablonu usługi Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 832c7831-d0e9-449b-b39c-9a09ba051531
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b2c962d5449d18b51cfd84b0e1992695b54d1c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-a-template"></a><span data-ttu-id="e48d0-103">Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="e48d0-103">Create User-Defined Routes (UDR) using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e48d0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e48d0-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="e48d0-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e48d0-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="e48d0-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="e48d0-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="e48d0-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e48d0-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="e48d0-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e48d0-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

> [!IMPORTANT]
> <span data-ttu-id="e48d0-109">Przed rozpoczęciem pracy z zasobami platformy Azure należy pamiętać, że ma ona obecnie dwa modele wdrażania: za pomocą usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="e48d0-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e48d0-110">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e48d0-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="e48d0-111">Dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty w górnej części artykułu.</span><span class="sxs-lookup"><span data-stu-id="e48d0-111">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="e48d0-112">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e48d0-112">This article covers the Resource Manager deployment model.</span></span> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

## <a name="udr-resources-in-a-template-file"></a><span data-ttu-id="e48d0-113">PRZEZ zasobów w pliku szablonu</span><span class="sxs-lookup"><span data-stu-id="e48d0-113">UDR resources in a template file</span></span>
<span data-ttu-id="e48d0-114">Można wyświetlić i pobrać [przykładowy szablon](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR).</span><span class="sxs-lookup"><span data-stu-id="e48d0-114">You can view and download the [sample template](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR).</span></span>

<span data-ttu-id="e48d0-115">W poniższej sekcji przedstawiono definicję frontonu przez w **azuredeploy-vnet-nsg-udr.json** pliku dla tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="e48d0-115">The following section shows the definition of the front-end UDR in the **azuredeploy-vnet-nsg-udr.json** file for the scenario:</span></span>

    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/routeTables",
    "name": "[parameters('frontEndRouteTableName')]",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "UDR - FrontEnd"   
    },
    "properties": {
      "routes": [
        {
          "name": "RouteToBackEnd",
          "properties": {
            "addressPrefix": "[parameters('backEndSubnetPrefix')]",
            "nextHopType": "VirtualAppliance",
            "nextHopIpAddress": "[parameters('vmaIpAddress')]"
          }
        }
      ]

<span data-ttu-id="e48d0-116">Aby skojarzyć przez podsieci frontonu, masz definicji podsieci w szablonie, a następnie użyj identyfikatora odwołania dla przez.</span><span class="sxs-lookup"><span data-stu-id="e48d0-116">To associate the UDR to the front-end subnet, you have to change the subnet definition in the template, and use the reference id for the UDR.</span></span>

    "subnets": [
        "name": "[parameters('frontEndSubnetName')]",
        "properties": {
          "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
          },
          "routeTable": {
              "id": "[resourceId('Microsoft.Network/routeTables', parameters('frontEndRouteTableName'))]"
          }
        },

<span data-ttu-id="e48d0-117">Zwróć uwagę, same wykonywana w ramach grupy NSG zaplecza i podsieć zaplecza w szablonie.</span><span class="sxs-lookup"><span data-stu-id="e48d0-117">Notice the same being done for the back-end NSG and the back-end subnet in the template.</span></span>

<span data-ttu-id="e48d0-118">Należy również upewnić się, że **FW1** maszyna wirtualna ma adres IP przekazywania właściwości włączony na karcie Sieciowej, która będzie służyć do pobierania i przekazywać pakiety.</span><span class="sxs-lookup"><span data-stu-id="e48d0-118">You also need to ensure that the **FW1** VM has the IP forwarding property enabled on the NIC that will be used to receive and forward packets.</span></span> <span data-ttu-id="e48d0-119">Poniższa sekcja przedstawia definicję karty interfejsu sieciowego dla FW1 w pliku azuredeploy-nsg-udr.json, oparta na scenariuszu powyżej.</span><span class="sxs-lookup"><span data-stu-id="e48d0-119">The section below shows the definition of the NIC for FW1 in the azuredeploy-nsg-udr.json file, based on the scenario above.</span></span>

    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DMZ"
    },
    "name": "[concat(variables('fwVMSettings').nicName, copyindex(1))]",
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('fwVMSettings').pipName, copyindex(1))]",
      "[concat('Microsoft.Resources/deployments/', 'vnetTemplate')]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "enableIPForwarding": true,
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat('192.168.0.',copyindex(4))]",
            "publicIPAddress": {
              "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('fwVMSettings').pipName, copyindex(1)))]"
            },
            "subnet": {
              "id": "[variables('dmzSubnetRef')]"
            }
          }
        }
      ]
    },
    "copy": {
      "name": "fwniccount",
      "count": "[parameters('fwCount')]"
    }

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="e48d0-120">Wdrażanie szablonu przy użyciu metody „kliknij, aby wdrożyć”</span><span class="sxs-lookup"><span data-stu-id="e48d0-120">Deploy the template by using click to deploy</span></span>
<span data-ttu-id="e48d0-121">Przykładowy szablon dostępny w repozytorium publicznym korzysta z pliku parametrów zawierającego wartości domyślne używane do generowania scenariusza opisanego powyżej.</span><span class="sxs-lookup"><span data-stu-id="e48d0-121">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="e48d0-122">Aby wdrożyć ten szablon przy użyciu metody „kliknij, aby wdrożyć”, kliknij [ten link](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR), kliknij przycisk **Deploy to Azure** (Wdróż na platformie Azure), w razie potrzeby zastąp wartości domyślne parametrów i postępuj zgodnie z instrukcjami podanymi w portalu.</span><span class="sxs-lookup"><span data-stu-id="e48d0-122">To deploy this template using click to deploy, follow [this link](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

1. <span data-ttu-id="e48d0-123">Jeśli nie znasz programu Azure PowerShell, zapoznaj się z artykułem [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i postępuj zgodnie z instrukcjami aż do momentu logowania się w programie Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e48d0-123">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="e48d0-124">Uruchom poniższe polecenie, aby utworzyć grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="e48d0-124">Run the following command to create a resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location westus
    ```

3. <span data-ttu-id="e48d0-125">Uruchom następujące polecenie, aby wdrożyć szablon:</span><span class="sxs-lookup"><span data-stu-id="e48d0-125">Run the following command to deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployUDR -ResourceGroupName TestRG `
        -TemplateUri https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json
    ```

    <span data-ttu-id="e48d0-126">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e48d0-126">Expected output:</span></span>
   
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
                            ASFW                Microsoft.Compute/availabilitySets       westus  
                            ASSQL               Microsoft.Compute/availabilitySets       westus  
                            ASWEB               Microsoft.Compute/availabilitySets       westus  
                            FW1                 Microsoft.Compute/virtualMachines        westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            WEB1                Microsoft.Compute/virtualMachines        westus  
                            WEB2                Microsoft.Compute/virtualMachines        westus  
                            NICFW1              Microsoft.Network/networkInterfaces      westus  
                            NICSQL1             Microsoft.Network/networkInterfaces      westus  
                            NICSQL2             Microsoft.Network/networkInterfaces      westus  
                            NICWEB1             Microsoft.Network/networkInterfaces      westus  
                            NICWEB2             Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            PIPFW1              Microsoft.Network/publicIPAddresses      westus  
                            PIPSQL1             Microsoft.Network/publicIPAddresses      westus  
                            PIPSQL2             Microsoft.Network/publicIPAddresses      westus  
                            PIPWEB1             Microsoft.Network/publicIPAddresses      westus  
                            PIPWEB2             Microsoft.Network/publicIPAddresses      westus  
                            UDR-BackEnd         Microsoft.Network/routeTables            westus  
                            UDR-FrontEnd        Microsoft.Network/routeTables            westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus

        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="e48d0-127">Wdrażanie szablonu przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e48d0-127">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="e48d0-128">Aby wdrożyć szablon ARM przy użyciu wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e48d0-128">To deploy the ARM template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="e48d0-129">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz artykuł [Instalowanie i konfigurowania interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) i postępuj zgodnie z instrukcjami aż do punktu, w którym należy wybrać konto platformy Azure i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="e48d0-129">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e48d0-130">Uruchom następujące polecenie, aby włączyć tryb Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="e48d0-130">Run the following command to switch to Resource Manager mode:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="e48d0-131">Oto oczekiwane dane wyjściowe po wprowadzeniu powyższego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e48d0-131">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="e48d0-132">W przeglądarce przejdź do **https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json**, a następnie skopiuj zawartość pliku json i wkleić do nowego pliku w sieci komputer.</span><span class="sxs-lookup"><span data-stu-id="e48d0-132">From your browser, navigate to **https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json**, copy the contents of the json file, and paste into a new file in your computer.</span></span> <span data-ttu-id="e48d0-133">W tym scenariuszu może być skopiowanie wartości poniżej w pliku o nazwie **c:\udr\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="e48d0-133">For this scenario, you would be copying the values below to a file named **c:\udr\azuredeploy.parameters.json**.</span></span>

    ```json
        {
          "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "fwCount": {
              "value": 1
            },
            "webCount": {
              "value": 2
            },
            "sqlCount": {
              "value": 2
            }
          }
        }
    ```

4. <span data-ttu-id="e48d0-134">Uruchom następujące polecenie, aby wdrożyć nową sieć wirtualną przy użyciu szablonu i parametr plików pobranego i zmodyfikowanego:</span><span class="sxs-lookup"><span data-stu-id="e48d0-134">Run the following command to deploy the new VNet by using the template and parameter files you downloaded and modified above:</span></span>

    ```azurecli
    azure group create -n TestRG -l westus --template-uri 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.json' -e 'c:\udr\azuredeploy.parameters.json'
    ```

    <span data-ttu-id="e48d0-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e48d0-135">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Updating resource group TestRG
        info:    Updated resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription Id]/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK

5. <span data-ttu-id="e48d0-136">Uruchom następujące polecenie, aby wyświetlić zasoby utworzone w nowej grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="e48d0-136">Run the following command to view the resources created in the new resource group:</span></span>

    ```azurecli
    azure group show TestRG
    ```

    <span data-ttu-id="e48d0-137">Oczekiwany wynik:</span><span class="sxs-lookup"><span data-stu-id="e48d0-137">Expected result:</span></span>

            info:    Executing command group show
            info:    Listing resource groups
            info:    Listing resources for the group
            data:    Id:                  /subscriptions/[Subscription Id]/resourceGroups/TestRG
            data:    Name:                TestRG
            data:    Location:            westus
            data:    Provisioning State:  Succeeded
            data:    Tags: null
            data:    Resources:
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASFW
            data:      Name    : ASFW
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASSQL
            data:      Name    : ASSQL
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASWEB
            data:      Name    : ASWEB
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1
            data:      Name    : FW1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/SQL1
            data:      Name    : SQL1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/SQL2
            data:      Name    : SQL2
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WEB1
            data:      Name    : WEB1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WEB2
            data:      Name    : WEB2
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
                data:      Name    : NICFW1
        data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1
            data:      Name    : NICSQL1
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2
            data:      Name    : NICSQL2
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1
            data:      Name    : NICWEB1
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2
            data:      Name    : NICWEB2
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd
            data:      Name    : NSG-BackEnd
            data:      Type    : networkSecurityGroups
            data:      Location: westus
            data:      Tags    : displayName=NSG - Front End
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
            data:      Name    : NSG-FrontEnd
            data:      Type    : networkSecurityGroups
            data:      Location: westus
            data:      Tags    : displayName=NSG - Remote Access
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1
            data:      Name    : PIPFW1
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPSQL1
            data:      Name    : PIPSQL1
                data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPSQL2
            data:      Name    : PIPSQL2
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
            data:      Name    : PIPWEB1
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPWEB2
            data:      Name    : PIPWEB2
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd
            data:      Name    : UDR-BackEnd
            data:      Type    : routeTables
            data:      Location: westus
            data:      Tags    : displayName=Route Table - Back End
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd
            data:      Name    : UDR-FrontEnd
            data:      Type    : routeTables
            data:      Location: westus
            data:      Tags    : displayName=UDR - FrontEnd
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
            data:      Name    : TestVNet
            data:      Type    : virtualNetworks
            data:      Location: westus
            data:      Tags    : displayName=VNet
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Storage/storageAccounts/testvnetstorageprm
            data:      Name    : testvnetstorageprm
            data:      Type    : storageAccounts
            data:      Location: westus
            data:      Tags    : displayName=Storage Account - Premium
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Storage/storageAccounts/testvnetstoragestd
            data:      Name    : testvnetstoragestd
            data:      Type    : storageAccounts
            data:      Location: westus
            data:      Tags    : displayName=Storage Account - Simple
            data:    
            data:    Permissions:
            data:      Actions: *
            data:      NotActions: 
            data:
            info:    group show command OK

> [!TIP]
> <span data-ttu-id="e48d0-138">Jeśli nie ma wszystkich zasobów, uruchom `azure group deployment show` polecenie, aby upewnić się, stan inicjowania wdrożenia jest *Succeded*.</span><span class="sxs-lookup"><span data-stu-id="e48d0-138">If you do not see all the resources, run the `azure group deployment show` command to ensure the provisioning state of the deployment is *Succeded*.</span></span>
> 
