---
title: Zestawy skalowania maszyny wirtualnej systemu Linux skalowania automatycznego | Dokumentacja firmy Microsoft
description: "Ustawienia skalowania automatycznego dla systemu Linux zestawu skalowania maszyn wirtualnych przy użyciu wiersza polecenia platformy Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: eff4add1cb16fe25022787668dc1d2277845dd95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="59a15-103">Automatycznie skalować maszyny z systemem Linux w zestawie skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="59a15-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="59a15-104">Zestawy skalowania maszyny wirtualnej ułatwiają wdrażanie i zarządzanie maszynami wirtualnymi identyczne jako zestaw.</span><span class="sxs-lookup"><span data-stu-id="59a15-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="59a15-105">Zestawy skalowania w przypadku aplikacji o dużej skali zapewnić warstwy obliczeniowej wysoce skalowalnemu i dostosowania i obsługują obrazów platformy systemu Windows, Linux platformy obrazów niestandardowych obrazów i rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="59a15-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="59a15-106">Aby dowiedzieć się więcej, zobacz [omówienie zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="59a15-107">W tym samouczku przedstawiono sposób tworzenia zestawu skalowania maszyn wirtualnych systemu Linux przy użyciu najnowszej wersji Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="59a15-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span></span> <span data-ttu-id="59a15-108">Samouczek przedstawia również sposób automatycznie skalować maszyn w zestawie.</span><span class="sxs-lookup"><span data-stu-id="59a15-108">The tutorial also shows you how to automatically scale the machines in the set.</span></span> <span data-ttu-id="59a15-109">Możesz utworzyć skalowalnego definiować skalowania przez utworzenie szablonu usługi Azure Resource Manager i wdrażanie za pomocą interfejsu wiersza polecenia Azure a.</span><span class="sxs-lookup"><span data-stu-id="59a15-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="59a15-110">Aby uzyskać więcej informacji na temat szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="59a15-111">Aby dowiedzieć się więcej na temat skalowania automatycznego zestawy skalowania, zobacz [automatyczne skalowanie i zestawach skali maszyny wirtualnej](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="59a15-112">W tym samouczku wdrażania następujących zasobów i rozszerzeń:</span><span class="sxs-lookup"><span data-stu-id="59a15-112">In this tutorial, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="59a15-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="59a15-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="59a15-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="59a15-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="59a15-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="59a15-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="59a15-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="59a15-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="59a15-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="59a15-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="59a15-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="59a15-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="59a15-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="59a15-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="59a15-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="59a15-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="59a15-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="59a15-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="59a15-122">Aby uzyskać więcej informacji na temat zasoby usługi Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="59a15-123">Przed rozpoczęciem kroków w tym samouczku [instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="59a15-124">Krok 1: Tworzenie grupy zasobów i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="59a15-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="59a15-125">**Zaloguj się do platformy Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="59a15-125">**Sign in to Microsoft Azure**</span></span>  
<span data-ttu-id="59a15-126">W interfejsie wiersza polecenia (Bash, terminali, wiersza polecenia), należy włączyć tryb Resource Manager, a następnie [Zaloguj się za pomocą identyfikatora firmy lub szkoły](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Postępuj zgodnie z monitami w celu obsługi logowania interakcyjnego do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59a15-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="59a15-127">Jeśli masz służbowego lub szkolnego identyfikator i nie mają włączone uwierzytelnianie dwuskładnikowe, użyj `azure login -u` o identyfikatorze można logować się bez sesji interaktywnej.</span><span class="sxs-lookup"><span data-stu-id="59a15-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span></span> <span data-ttu-id="59a15-128">Jeśli nie ma służbowego lub szkolnego identyfikator, możesz [Utwórz identyfikator firmy lub szkoły z osobistego konta Microsoft](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="59a15-129">**Utwórz grupę zasobów**</span><span class="sxs-lookup"><span data-stu-id="59a15-129">**Create a resource group**</span></span>  
<span data-ttu-id="59a15-130">Należy wdrożyć wszystkie zasoby w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="59a15-130">All resources must be deployed to a resource group.</span></span> <span data-ttu-id="59a15-131">W tym samouczku, określ nazwę grupy zasobów **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="59a15-131">For this tutorial, name the resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="59a15-132">**Wdrażanie konta magazynu do nowej grupy zasobów**</span><span class="sxs-lookup"><span data-stu-id="59a15-132">**Deploy a storage account into the new resource group**</span></span>  
<span data-ttu-id="59a15-133">To konto magazynu jest przechowywania szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-133">This storage account is where the template is stored.</span></span> <span data-ttu-id="59a15-134">Utwórz konto magazynu o nazwie **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="59a15-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-the-template"></a><span data-ttu-id="59a15-135">Krok 2: Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="59a15-135">Step 2: Create the template</span></span>
<span data-ttu-id="59a15-136">Szablon usługi Azure Resource Manager umożliwia do wdrażania i zarządzania zasobami Azure ze sobą przy użyciu opisu JSON zasobów i parametrów skojarzonego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="59a15-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="59a15-137">W edytorze Ulubione Utwórz plik VMSSTemplate.json i Dodaj początkowej strukturze JSON do obsługi szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="59a15-138">Parametry nie są zawsze wymagana, ale umożliwiają wprowadzanie wartości podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="59a15-139">Dodaj tych parametrów w obszarze parametrów elementu nadrzędnego, który został dodany do szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-139">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="59a15-140">Ustaw nazwę oddzielne maszynę wirtualną, która umożliwia dostęp do maszyn w skali.</span><span class="sxs-lookup"><span data-stu-id="59a15-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
   * <span data-ttu-id="59a15-141">Nazwa konta magazynu, w którym szablon jest przechowywany.</span><span class="sxs-lookup"><span data-stu-id="59a15-141">A name for the storage account where the template is stored.</span></span>
   * <span data-ttu-id="59a15-142">Liczba wystąpień maszyn wirtualnych można początkowo utworzyć w skali zestawu.</span><span class="sxs-lookup"><span data-stu-id="59a15-142">The number of instances of virtual machines to initially create in the scale set.</span></span>
   * <span data-ttu-id="59a15-143">Nazwa i hasło konta administratora na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="59a15-143">A name and password of the administrator account on the virtual machines.</span></span>
   * <span data-ttu-id="59a15-144">Prefiks nazwy zasobów, które są tworzone w celu obsługi zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="59a15-144">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="59a15-145">Zmienne można w szablonie, aby określić wartości, które mogą ulec zmianie często lub wartości, które muszą zostać utworzone z kombinacji wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="59a15-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="59a15-146">Dodaj te zmienne w obszarze Zmienne elementu nadrzędnego, który został dodany do szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-146">Add these variables under the variables parent element that you added to the template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="59a15-147">Nazwy DNS, które są używane przez interfejsy sieciowe.</span><span class="sxs-lookup"><span data-stu-id="59a15-147">DNS names that are used by the network interfaces.</span></span>
   * <span data-ttu-id="59a15-148">Nazwy adresów IP i prefiksy dla sieci wirtualnej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="59a15-148">The IP address names and prefixes for the virtual network and subnets.</span></span>
   * <span data-ttu-id="59a15-149">Nazwy i identyfikatory sieci wirtualnej załadować równoważenia i interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="59a15-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="59a15-150">Ustawianie nazw kont magazynu dla konta skojarzone z maszyn w skali.</span><span class="sxs-lookup"><span data-stu-id="59a15-150">Storage account names for the accounts associated with the machines in the scale set.</span></span>
   * <span data-ttu-id="59a15-151">Ustawienia rozszerzenia diagnostyki, które jest zainstalowane na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="59a15-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="59a15-152">Aby uzyskać więcej informacji na temat rozszerzenia diagnostyki, zobacz [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59a15-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="59a15-153">Dodaj zasób konta magazynu w zasoby elementu nadrzędnego, który został dodany do szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-153">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="59a15-154">Ten szablon używa pętlę do utworzenia zalecane pięć kont magazynu przechowywania dysków systemu operacyjnego i danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="59a15-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="59a15-155">Ten zestaw kont może obsługiwać maksymalnie 100 maszyn wirtualnych w zestawie skalowania, który jest bieżącym maksymalną.</span><span class="sxs-lookup"><span data-stu-id="59a15-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="59a15-156">Każde konto magazynu ma nazwę z określeniem litera, która została zdefiniowana w zmiennych, w połączeniu z sufiksem parametry podane dla szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span></span>
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. <span data-ttu-id="59a15-157">Dodaj zasób sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="59a15-157">Add the virtual network resource.</span></span> <span data-ttu-id="59a15-158">Aby uzyskać więcej informacji, zobacz [dostawcy zasobów sieciowych](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="59a15-159">Dodaj zasoby publicznych adresów IP, które są używane przez usługi równoważenia obciążenia i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="59a15-159">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="59a15-160">Dodaj zasób usługi równoważenia obciążenia, który jest używany przez zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="59a15-160">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="59a15-161">Aby uzyskać więcej informacji, zobacz [Obsługa Menedżera zasobów Azure dla usługi równoważenia obciążenia](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="59a15-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="59a15-162">Dodaj zasób interfejsu sieci, który jest używany przez oddzielne maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="59a15-162">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="59a15-163">Ponieważ maszyny w zestawie skalowania nie są dostępne za pośrednictwem publicznego adresu IP, oddzielnej maszynie wirtualnej jest tworzony w tej samej sieci wirtualnej do dostępu zdalnego do maszyny.</span><span class="sxs-lookup"><span data-stu-id="59a15-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="59a15-164">Dodaj oddzielnej maszynie wirtualnej w tej samej sieci co zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="59a15-164">Add the separate virtual machine in the same network as the scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="59a15-165">Dodaj zasób zestawu skalowania maszyny wirtualnej i określ rozszerzenie diagnostyki, który jest zainstalowany na wszystkich maszynach wirtualnych w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="59a15-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="59a15-166">Wiele ustawień dla tego zasobu przypominają z zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="59a15-166">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="59a15-167">Główne różnice są element pojemności, który określa liczbę maszyn wirtualnych w zestawie skali i upgradePolicy, która określa, jak zostało zaktualizowane do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="59a15-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="59a15-168">Zestaw skalowania nie jest tworzony, dopóki wszystkie konta magazynu są tworzone za pomocą elementu dependsOn określonej.</span><span class="sxs-lookup"><span data-stu-id="59a15-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="59a15-169">Dodaj zasób autoscaleSettings, który definiuje sposób oparte na wykorzystanie procesora na komputerach w zestawie dopasowuje zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="59a15-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    <span data-ttu-id="59a15-170">W tym samouczku te wartości są ważne:</span><span class="sxs-lookup"><span data-stu-id="59a15-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="59a15-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="59a15-171">**metricName**</span></span>  
    <span data-ttu-id="59a15-172">Ta wartość jest taka sama jak zdefiniowanego w zmiennej wadperfcounter licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="59a15-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="59a15-173">Za pomocą tej zmiennej, zbiera rozszerzenia diagnostyki **Processor\PercentProcessorTime** licznika.</span><span class="sxs-lookup"><span data-stu-id="59a15-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="59a15-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="59a15-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="59a15-175">Ta wartość jest identyfikator zasobu zestawu skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="59a15-175">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="59a15-176">**ziarnem czasu**</span><span class="sxs-lookup"><span data-stu-id="59a15-176">**timeGrain**</span></span>  
    <span data-ttu-id="59a15-177">Ta wartość jest stopień szczegółowości metryki, które są zbierane.</span><span class="sxs-lookup"><span data-stu-id="59a15-177">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="59a15-178">W tym szablonie ustawiono na jedną minutę.</span><span class="sxs-lookup"><span data-stu-id="59a15-178">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="59a15-179">**Statystyka**</span><span class="sxs-lookup"><span data-stu-id="59a15-179">**statistic**</span></span>  
    <span data-ttu-id="59a15-180">Ta wartość określa, jak metryki połączone pomieścić automatycznych akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="59a15-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="59a15-181">Możliwe wartości to: średnia, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="59a15-181">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="59a15-182">W tym szablonie są zbierane średniego użycia procesora CPU całkowity maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="59a15-182">In this template, the average total CPU usage of the virtual machines is collected.</span></span>

    * <span data-ttu-id="59a15-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="59a15-183">**timeWindow**</span></span>  
    <span data-ttu-id="59a15-184">Ta wartość jest przedział czasu, w którym są zbierane dane wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="59a15-184">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="59a15-185">Musi być od 5 minut do 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="59a15-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="59a15-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="59a15-186">**timeAggregation**</span></span>  
    <span data-ttu-id="59a15-187">jego wartość określa, jak powinny być połączone dane, które są zbierane wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="59a15-187">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="59a15-188">Wartość domyślna to średnia.</span><span class="sxs-lookup"><span data-stu-id="59a15-188">The default value is Average.</span></span> <span data-ttu-id="59a15-189">Możliwe wartości to: średnia, co najmniej, maksimum, ostatnich, łączna liczba, liczba.</span><span class="sxs-lookup"><span data-stu-id="59a15-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="59a15-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="59a15-190">**operator**</span></span>  
    <span data-ttu-id="59a15-191">Ta wartość jest operator, który służy do porównywania danych metryki i wartość progową.</span><span class="sxs-lookup"><span data-stu-id="59a15-191">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="59a15-192">Możliwe wartości to: równa, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="59a15-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="59a15-193">**Próg**</span><span class="sxs-lookup"><span data-stu-id="59a15-193">**threshold**</span></span>  
    <span data-ttu-id="59a15-194">Ta wartość jest wyzwalane akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="59a15-194">This value triggers the scale action.</span></span> <span data-ttu-id="59a15-195">W tym szablonie maszyn są dodawane do skalowania, ustawić, gdy średniego użycia procesora CPU między maszynami w zestawie jest ponad 50%.</span><span class="sxs-lookup"><span data-stu-id="59a15-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="59a15-196">**Kierunek**</span><span class="sxs-lookup"><span data-stu-id="59a15-196">**direction**</span></span>  
    <span data-ttu-id="59a15-197">Ta wartość Określa akcję wykonywaną, gdy uzyskuje się wartość progową.</span><span class="sxs-lookup"><span data-stu-id="59a15-197">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="59a15-198">Możliwe wartości to zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="59a15-198">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="59a15-199">W tym szablonie jeśli próg wynosi ponad 50% w oknie zdefiniowanego czasu zwiększa się liczba maszyn wirtualnych w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="59a15-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>

    * <span data-ttu-id="59a15-200">**Typ**</span><span class="sxs-lookup"><span data-stu-id="59a15-200">**type**</span></span>  
    <span data-ttu-id="59a15-201">Ta wartość jest typu akcji, która powinna się odbyć i musi mieć ustawioną ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="59a15-201">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="59a15-202">**wartość**</span><span class="sxs-lookup"><span data-stu-id="59a15-202">**value**</span></span>  
    <span data-ttu-id="59a15-203">Ta wartość jest liczba maszyn wirtualnych, które są dodawane lub usuwane z zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="59a15-203">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="59a15-204">Ta wartość musi wynosić 1 lub większą.</span><span class="sxs-lookup"><span data-stu-id="59a15-204">This value must be 1 or greater.</span></span> <span data-ttu-id="59a15-205">Wartość domyślna to 1.</span><span class="sxs-lookup"><span data-stu-id="59a15-205">The default value is 1.</span></span> <span data-ttu-id="59a15-206">W tym szablonie liczba maszyn w skali ustawić zwiększa 1, gdy ze osiągnięty jest próg.</span><span class="sxs-lookup"><span data-stu-id="59a15-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>

    * <span data-ttu-id="59a15-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="59a15-207">**cooldown**</span></span>  
    <span data-ttu-id="59a15-208">Ta wartość jest czas oczekiwania od momentu ostatniej akcji skalowania, zanim nastąpi następnej akcji.</span><span class="sxs-lookup"><span data-stu-id="59a15-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="59a15-209">Ta wartość musi należeć do zakresu od minutę i jeden tydzień.</span><span class="sxs-lookup"><span data-stu-id="59a15-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="59a15-210">Zapisz plik szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-210">Save the template file.</span></span>    

## <a name="step-3-upload-the-template-to-storage"></a><span data-ttu-id="59a15-211">Krok 3: Przekaż szablon do magazynu</span><span class="sxs-lookup"><span data-stu-id="59a15-211">Step 3: Upload the template to storage</span></span>
<span data-ttu-id="59a15-212">Szablon można przekazać tak długo, jak znać nazwy i klucza podstawowego konta magazynu, który został utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="59a15-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="59a15-213">W interfejsie wiersza polecenia (Bash, terminali, wiersza polecenia) uruchom następujące polecenia, aby ustawić zmienne środowiskowe wymagane do uzyskania dostępu do konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="59a15-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="59a15-214">Klucz można uzyskać, klikając ikonę klucza, podczas wyświetlania zasobów konta magazynu w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59a15-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span> <span data-ttu-id="59a15-215">Korzystając z wiersza polecenia systemu Windows, wpisz **ustawić** zamiast eksportu.</span><span class="sxs-lookup"><span data-stu-id="59a15-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="59a15-216">Utwórz kontener do przechowywania szablonu.</span><span class="sxs-lookup"><span data-stu-id="59a15-216">Create the container for storing the template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="59a15-217">Przekaż plik szablonu na nowy kontener.</span><span class="sxs-lookup"><span data-stu-id="59a15-217">Upload the template file to the new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-the-template"></a><span data-ttu-id="59a15-218">Krok 4: Wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="59a15-218">Step 4: Deploy the template</span></span>
<span data-ttu-id="59a15-219">Teraz, gdy szablon został utworzony, możesz przystąpić do wdrażania zasobów.</span><span class="sxs-lookup"><span data-stu-id="59a15-219">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="59a15-220">Użyj tego polecenia, aby rozpocząć proces:</span><span class="sxs-lookup"><span data-stu-id="59a15-220">Use this command to start the process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="59a15-221">Po naciśnięciu wprowadź, zostanie wyświetlony monit o podanie wartości zmiennych, które zostanie przypisane.</span><span class="sxs-lookup"><span data-stu-id="59a15-221">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="59a15-222">Podaj następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="59a15-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="59a15-223">Powinna ona potrwać około 15 minut dla wszystkich zasobów do wdrożenia pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="59a15-223">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="59a15-224">Można także użyć możliwości portalu do wdrażania zasobów.</span><span class="sxs-lookup"><span data-stu-id="59a15-224">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="59a15-225">Użyj tego linku: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="59a15-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="59a15-226">Krok 5: Monitorowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="59a15-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="59a15-227">Można uzyskać informacji o zestawy skalowania maszyny wirtualnej za pomocą następujących metod:</span><span class="sxs-lookup"><span data-stu-id="59a15-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="59a15-228">Portal Azure — można obecnie uzyskać ograniczoną ilość informacji za pomocą portalu.</span><span class="sxs-lookup"><span data-stu-id="59a15-228">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="59a15-229">[Eksploratora zasobów Azure](https://resources.azure.com/) — to narzędzie jest najlepszy do eksplorowania bieżącego stanu sieci zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="59a15-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="59a15-230">Tej ścieżki i powinien zostać wyświetlony widok wystąpienia zestawu skali utworzony:</span><span class="sxs-lookup"><span data-stu-id="59a15-230">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="59a15-231">Azure CLI — Użyj tego polecenia, aby pobrać niektóre informacje:</span><span class="sxs-lookup"><span data-stu-id="59a15-231">Azure CLI - Use this command to get some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="59a15-232">Połączenie z maszyną wirtualną jumpbox podobnie jak inne maszyny, a następnie zdalny dostęp maszyny wirtualne w skali ustawioną monitorowania poszczególnych procesów.</span><span class="sxs-lookup"><span data-stu-id="59a15-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="59a15-233">Zakończenie interfejsu API REST do uzyskiwania informacji na temat zestawów skalowania można znaleźć w [zestawach skali maszyny wirtualnej](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="59a15-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-the-resources"></a><span data-ttu-id="59a15-234">Krok 6: Usuń zasoby</span><span class="sxs-lookup"><span data-stu-id="59a15-234">Step 6: Remove the resources</span></span>
<span data-ttu-id="59a15-235">Ponieważ naliczane są opłaty za zasoby używane na platformie Azure, zawsze jest dobrym rozwiązaniem, aby usunąć zasoby, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="59a15-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="59a15-236">Nie trzeba osobno usunąć wszystkie zasoby w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="59a15-236">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="59a15-237">Można usunąć grupy zasobów i wszystkie jej zasoby są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="59a15-237">You can delete the resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="59a15-238">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59a15-238">Next steps</span></span>
* <span data-ttu-id="59a15-239">Znajdź przykłady Azure Monitor funkcje w [Azure Monitor i platform interfejsu wiersza polecenia Szybki start — przykłady](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="59a15-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="59a15-240">Dowiedz się więcej o funkcji powiadomień w [użyć akcji skalowania automatycznego do wysyłania wiadomości e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="59a15-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="59a15-241">Dowiedz się, jak [dzienników inspekcji używany do wysyłania wiadomości e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="59a15-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="59a15-242">Zapoznaj się z [aplikacja demonstracyjna skalowania automatycznego na Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) szablonu, który konfiguruje aplikacji Python/bottle do wykonywania funkcji skalowania automatycznego programu zestawach skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="59a15-242">Check out the [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

