---
title: aaaAutoscale zestawy skalowania maszyny wirtualnej z systemem Windows | Dokumentacja firmy Microsoft
description: "Ustawienia skalowania automatycznego dla systemu Windows zestawu skalowania maszyn wirtualnych przy użyciu programu Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="b2c27-103">Automatycznie skalować maszyny w zestawie skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="b2c27-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="b2c27-104">Zestawy skalowania maszyn wirtualnych ułatwiają możesz toodeploy i zarządzaj nimi wiele identycznych maszyn wirtualnych jako zestaw.</span><span class="sxs-lookup"><span data-stu-id="b2c27-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="b2c27-105">Zestawy skalowania w przypadku aplikacji o dużej skali zapewnić warstwy obliczeniowej wysoce skalowalnemu i dostosowania i obsługują obrazów platformy systemu Windows, Linux platformy obrazów niestandardowych obrazów i rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b2c27-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="b2c27-106">Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawach skali maszyny wirtualnej](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2c27-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="b2c27-107">Ten samouczek pokazuje, jak ustawić toocreate zestaw skalowania maszyn wirtualnych Windows i automatycznie skali hello maszyn w hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="b2c27-108">Możesz utworzyć hello skalowalnego definiować skalowania przez utworzenie szablonu usługi Azure Resource Manager i wdrażania go przy użyciu programu Azure PowerShell a.</span><span class="sxs-lookup"><span data-stu-id="b2c27-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="b2c27-109">Aby uzyskać więcej informacji na temat szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b2c27-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="b2c27-110">toolearn więcej informacji na temat skalowania automatycznego zestawy skalowania, zobacz [automatyczne skalowanie i zestawach skali maszyny wirtualnej](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2c27-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="b2c27-111">W tym artykule wdrożeniem hello następujących zasobów i rozszerzeń:</span><span class="sxs-lookup"><span data-stu-id="b2c27-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="b2c27-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="b2c27-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="b2c27-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="b2c27-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="b2c27-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="b2c27-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="b2c27-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="b2c27-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="b2c27-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="b2c27-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="b2c27-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="b2c27-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="b2c27-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="b2c27-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="b2c27-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="b2c27-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="b2c27-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="b2c27-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="b2c27-121">Aby uzyskać więcej informacji na temat zasoby usługi Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b2c27-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="b2c27-122">Krok 1. Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2c27-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="b2c27-123">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b2c27-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="b2c27-124">Krok 2: Tworzenie grupy zasobów i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="b2c27-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="b2c27-125">**Utwórz grupę zasobów** — wszystkie zasoby musi być wdrożone tooa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b2c27-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="b2c27-126">Użyj [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate grupę zasobów o nazwie **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="b2c27-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="b2c27-127">**Utwórz konto magazynu** — to konto magazynu jest przechowywania hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="b2c27-128">Użyj [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate konto magazynu o nazwie **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="b2c27-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="b2c27-129">Krok 3: Tworzenie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="b2c27-129">Step 3: Create hello template</span></span>
<span data-ttu-id="b2c27-130">Szablonu usługi Azure Resource Manager umożliwia możesz toodeploy i zarządzania zasobami Azure ze sobą przy użyciu opisu JSON zasobów hello i parametry skojarzonego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b2c27-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="b2c27-131">W edytorze Ulubione Utwórz plik hello C:\VMSSTemplate.json i Dodaj hello początkowej JSON struktury toosupport hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="b2c27-132">Parametry nie są zawsze wymagana, ale ich tooinput sposób wartości po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="b2c27-133">Dodaj tych parametrów w obszarze hello elementu nadrzędnego dla parametrów czy dodany szablon toohello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="b2c27-134">Nazwa dla hello oddzielne maszyny wirtualnej, która jest używana tooaccess hello maszyny w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="b2c27-135">Hello nazwa konta magazynu hello przechowywania hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="b2c27-136">Utwórz Hello liczba tooinitially maszyn wirtualnych w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="b2c27-137">Witaj nazwę i hasło konta administratora hello na maszynach wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="b2c27-138">Ustaw prefiksu nazwy hello zasobów, które są tworzone toosupport hello skali.</span><span class="sxs-lookup"><span data-stu-id="b2c27-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="b2c27-139">Zmienne mogą być używane w wartości toospecify szablonów, które mogą ulec zmianie często lub wartości, które wymagają toobe utworzone na podstawie kombinację wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="b2c27-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="b2c27-140">Dodaj te zmienne w obszarze elementu nadrzędnego zmienne hello czy dodany szablon toohello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="b2c27-141">Nazwy DNS, które są używane przez hello interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="b2c27-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="b2c27-142">Witaj nazwy adresów IP i prefiksy hello sieci wirtualnej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="b2c27-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="b2c27-143">Witaj nazwy i identyfikatory hello sieci wirtualnej, obciążenia równoważenia i interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="b2c27-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="b2c27-144">Nazwy konta magazynu dla konta hello skojarzone z hello maszyny w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="b2c27-145">Ustawienia dla hello diagnostyki rozszerzenia, które jest zainstalowane na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="b2c27-146">Aby uzyskać więcej informacji na temat hello rozszerzenia diagnostyki, zobacz [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2c27-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="b2c27-147">Dodaj zasób konta magazynu hello pod elementem nadrzędnym zasobów hello czy dodany szablon toohello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="b2c27-148">Ten szablon używa hello toocreate pętli, zalecane konta magazynu przechowywania hello dysków systemu operacyjnego i danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="b2c27-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="b2c27-149">Ten zestaw kont może obsługiwać zapasowych too100 maszyn wirtualnych w zestawie skalowania jest bieżąca maksymalna hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="b2c27-150">Z określeniem litera, która została zdefiniowana w połączeniu z hello prefiks hello parametrów szablonu hello zmiennych hello nosi nazwę każdego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

    ```json
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
    ```

5. <span data-ttu-id="b2c27-151">Dodaj hello zasobów sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2c27-151">Add hello virtual network resource.</span></span> <span data-ttu-id="b2c27-152">Aby uzyskać więcej informacji, zobacz [dostawcy zasobów sieciowych](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="b2c27-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="b2c27-153">Dodaj hello publicznego zasoby adresów IP używanych przez hello obciążenia równoważenia i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b2c27-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="b2c27-154">Dodaj zasób usługi równoważenia obciążenia hello, który jest używany przez zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="b2c27-155">Aby uzyskać więcej informacji, zobacz [Obsługa Menedżera zasobów Azure dla usługi równoważenia obciążenia](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b2c27-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="b2c27-156">Dodaj hello sieci interfejsu zasób, który jest używany przez maszynę wirtualną z oddzielnych hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="b2c27-157">Ponieważ maszyny w zestawie skalowania nie są dostępne za pośrednictwem publicznego adresu IP, oddzielnej maszynie wirtualnej jest tworzony w hello sam wirtualnych sieci tooremotely dostępu hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="b2c27-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="b2c27-158">Dodaj hello oddzielnej maszynie wirtualnej w hello sam sieci jako zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
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

10. <span data-ttu-id="b2c27-159">Dodaj zasób zestawu skalowania maszyny wirtualnej hello i określ hello diagnostyki rozszerzenia, które jest zainstalowany na wszystkich maszynach wirtualnych w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="b2c27-160">Wiele ustawień powitania dla tego zasobu przypominają z hello zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2c27-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="b2c27-161">główne różnice Hello są hello pojemność elementu, który określa hello liczbę maszyn wirtualnych w zestawie skalowania hello i upgradePolicy określający, jak zaktualizowane toovirtual maszyny.</span><span class="sxs-lookup"><span data-stu-id="b2c27-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="b2c27-162">Witaj zestaw skalowania jest tworzone dopiero po wszystkich kont magazynu hello są tworzone z elementem dependsOn hello określonej.</span><span class="sxs-lookup"><span data-stu-id="b2c27-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
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
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="b2c27-163">Dodaj hello autoscaleSettings zasób, który definiuje sposób oparte na powitania wykorzystanie procesora na komputerach hello w zestawie skalowania hello dopasowuje zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

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
                  "metricName": "\\Processor(_Total)\\% Processor Time",
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

    <span data-ttu-id="b2c27-164">W tym samouczku te wartości są ważne:</span><span class="sxs-lookup"><span data-stu-id="b2c27-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="b2c27-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="b2c27-165">**metricName**</span></span>  
    <span data-ttu-id="b2c27-166">Ta wartość jest hello taki sam jak hello licznika wydajności, zdefiniowanego w zmiennej wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="b2c27-167">Za pomocą tej zmiennej, hello rozszerzenia diagnostycznych zbiera hello **procesor(_Total)\% czasu procesora** licznika.</span><span class="sxs-lookup"><span data-stu-id="b2c27-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="b2c27-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="b2c27-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="b2c27-169">Ta wartość jest identyfikator zasobu hello zestaw skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="b2c27-170">**ziarnem czasu**</span><span class="sxs-lookup"><span data-stu-id="b2c27-170">**timeGrain**</span></span>  
    <span data-ttu-id="b2c27-171">Ta wartość jest szczegółowości hello hello metryk, które są zbierane.</span><span class="sxs-lookup"><span data-stu-id="b2c27-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="b2c27-172">W tym szablonie ustawiono tooone minutę.</span><span class="sxs-lookup"><span data-stu-id="b2c27-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="b2c27-173">**Statystyka**</span><span class="sxs-lookup"><span data-stu-id="b2c27-173">**statistic**</span></span>  
    <span data-ttu-id="b2c27-174">Ta wartość określa, jak metryki hello są połączone tooaccommodate hello automatyczne skalowanie akcji.</span><span class="sxs-lookup"><span data-stu-id="b2c27-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="b2c27-175">Witaj możliwe wartości to: średnia, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="b2c27-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="b2c27-176">W tym szablonie są zbierane hello średni całkowite użycie Procesora hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b2c27-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="b2c27-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="b2c27-177">**timeWindow**</span></span>  
    <span data-ttu-id="b2c27-178">Ta wartość jest hello zakres czasu, w którym są zbierane dane wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b2c27-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="b2c27-179">Musi być od 5 minut do 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="b2c27-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="b2c27-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="b2c27-180">**timeAggregation**</span></span>  
    <span data-ttu-id="b2c27-181">jego wartość określa, jak powinny być połączone hello dane, które są zbierane wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="b2c27-182">Witaj domyślna wartość to średnia.</span><span class="sxs-lookup"><span data-stu-id="b2c27-182">hello default value is Average.</span></span> <span data-ttu-id="b2c27-183">Witaj możliwe wartości to: średnia, co najmniej, maksimum, ostatnich, łączna liczba, liczba.</span><span class="sxs-lookup"><span data-stu-id="b2c27-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="b2c27-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="b2c27-184">**operator**</span></span>  
    <span data-ttu-id="b2c27-185">Ta wartość jest hello operator, który jest używany toocompare hello metryki danych i hello próg.</span><span class="sxs-lookup"><span data-stu-id="b2c27-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="b2c27-186">Witaj możliwe wartości to: równa, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="b2c27-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="b2c27-187">**Próg**</span><span class="sxs-lookup"><span data-stu-id="b2c27-187">**threshold**</span></span>  
    <span data-ttu-id="b2c27-188">Ta wartość jest wartość hello wyzwala hello akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="b2c27-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="b2c27-189">W tym szablonie maszyn dodanych skali toohello ustawić, gdy hello średniego użycia procesora CPU między maszynami w zestawie hello jest ponad 50%.</span><span class="sxs-lookup"><span data-stu-id="b2c27-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="b2c27-190">**Kierunek**</span><span class="sxs-lookup"><span data-stu-id="b2c27-190">**direction**</span></span>  
    <span data-ttu-id="b2c27-191">Ta wartość określa akcji hello, wykonywaną, gdy uzyskuje się hello wartość progową.</span><span class="sxs-lookup"><span data-stu-id="b2c27-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="b2c27-192">Witaj możliwe wartości to zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="b2c27-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="b2c27-193">W tym szablonie hello liczbę maszyn wirtualnych w zestawie skalowania hello jest zwiększane, gdy próg hello jest ponad 50% hello określone okno czasu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="b2c27-194">**Typ**</span><span class="sxs-lookup"><span data-stu-id="b2c27-194">**type**</span></span>  
    <span data-ttu-id="b2c27-195">Ta wartość jest typu hello akcji, która powinna się odbyć i musi być ustawione tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="b2c27-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="b2c27-196">**wartość**</span><span class="sxs-lookup"><span data-stu-id="b2c27-196">**value**</span></span>  
    <span data-ttu-id="b2c27-197">Ta wartość jest liczbą hello maszyn wirtualnych, które zostały dodane lub usunięte z hello zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="b2c27-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="b2c27-198">Ta wartość musi wynosić 1 lub większą.</span><span class="sxs-lookup"><span data-stu-id="b2c27-198">This value must be 1 or greater.</span></span> <span data-ttu-id="b2c27-199">Witaj, wartość domyślna to 1.</span><span class="sxs-lookup"><span data-stu-id="b2c27-199">hello default value is 1.</span></span> <span data-ttu-id="b2c27-200">W tym szablonie hello liczba maszyn w skali hello ustawić zwiększa 1, gdy zostały spełnione warunki progowe hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="b2c27-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="b2c27-201">**cooldown**</span></span>  
    <span data-ttu-id="b2c27-202">Ta wartość jest hello ilość czasu toowait od momentu ostatniej akcji skalowania hello, zanim nastąpi hello następnej akcji.</span><span class="sxs-lookup"><span data-stu-id="b2c27-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="b2c27-203">Ta wartość musi należeć do zakresu od minutę i jeden tydzień.</span><span class="sxs-lookup"><span data-stu-id="b2c27-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="b2c27-204">Zapisz plik szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="b2c27-205">Krok 4: Przekaż hello toostorage szablonu</span><span class="sxs-lookup"><span data-stu-id="b2c27-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="b2c27-206">można przekazać szablon Hello tak długo, jak znana nazwa hello i klucz podstawowy hello konta magazynu, który został utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="b2c27-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="b2c27-207">W oknie programu PowerShell Azure Microsoft hello wartość zmiennej, która określa nazwę hello hello konta magazynu, który został utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="b2c27-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="b2c27-208">Wartość zmiennej, która określa klucz podstawowy hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2c27-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="b2c27-209">Ten klucz można uzyskać, klikając ikonę klucza hello podczas wyświetlania zasobów konta magazynu hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c27-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="b2c27-210">Utworzyć obiekt kontekstu konta magazynu hello, będącą operacji toovalidate używanych z kontem magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="b2c27-211">Tworzenie kontenera hello do przechowywania szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="b2c27-212">Przekaż hello szablon pliku toohello nowego kontenera.</span><span class="sxs-lookup"><span data-stu-id="b2c27-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="b2c27-213">Krok 5: Wdrożenie hello szablonu</span><span class="sxs-lookup"><span data-stu-id="b2c27-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="b2c27-214">Teraz, gdy utworzono szablon hello, możesz przystąpić do wdrażania hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="b2c27-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="b2c27-215">Użyj tego polecenia toostart hello procesu:</span><span class="sxs-lookup"><span data-stu-id="b2c27-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="b2c27-216">Po naciśnięciu wprowadź, zostanie wyświetlony monit o tooprovide wartości zmiennych hello, przypisana.</span><span class="sxs-lookup"><span data-stu-id="b2c27-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="b2c27-217">Podaj następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="b2c27-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="b2c27-218">Dla wszystkich toosuccessfully zasobów hello można wdrożyć powinien trwa około 15 minut.</span><span class="sxs-lookup"><span data-stu-id="b2c27-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="b2c27-219">Umożliwia także hello portal możliwości toodeploy hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="b2c27-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="b2c27-220">Użyj tego linku: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span><span class="sxs-lookup"><span data-stu-id="b2c27-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="b2c27-221">Krok 6: Monitor zasobów</span><span class="sxs-lookup"><span data-stu-id="b2c27-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="b2c27-222">Można uzyskać informacji o zestawy skalowania maszyny wirtualnej za pomocą następujących metod:</span><span class="sxs-lookup"><span data-stu-id="b2c27-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="b2c27-223">Witaj Azure portal — można obecnie uzyskać ograniczoną ilość informacji za pomocą portalu hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="b2c27-224">Witaj [Eksploratora zasobów Azure](https://resources.azure.com/) — narzędzie to jest hello najlepsze do eksplorowania hello bieżącego stanu sieci zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="b2c27-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="b2c27-225">Tej ścieżki i powinna zostać wyświetlona zestawu widok wystąpienia hello skali hello utworzony:</span><span class="sxs-lookup"><span data-stu-id="b2c27-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="b2c27-226">Subskrypcje > {subskrypcji} > resourceGroups > vmsstestrg1 > dostawców > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="b2c27-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="b2c27-227">Program Azure PowerShell — Użyj tego polecenia tooget niektóre informacje:</span><span class="sxs-lookup"><span data-stu-id="b2c27-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="b2c27-228">Lub</span><span class="sxs-lookup"><span data-stu-id="b2c27-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="b2c27-229">Połącz toohello oddzielnej maszynie wirtualnej, podobnie jak inne maszyny, a następnie można zdalnie przejść hello maszyn wirtualnych w hello skali zestaw toomonitor poszczególnych procesów.</span><span class="sxs-lookup"><span data-stu-id="b2c27-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="b2c27-230">Zakończenie interfejsu API REST do uzyskiwania informacji na temat zestawów skalowania można znaleźć w [zestawach skali maszyny wirtualnej](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="b2c27-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="b2c27-231">Krok 7: Usuwanie hello zasobów</span><span class="sxs-lookup"><span data-stu-id="b2c27-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="b2c27-232">Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="b2c27-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="b2c27-233">Nie trzeba toodelete każdego zasobu niezależnie od grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b2c27-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="b2c27-234">Można usunąć grupy zasobów hello i wszystkie jej zasoby są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="b2c27-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="b2c27-235">Jeśli chcesz tookeep w grupie zasobów, można usunąć tylko zestaw skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="b2c27-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="b2c27-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2c27-236">Next steps</span></span>
* <span data-ttu-id="b2c27-237">Zarządzanie hello zestaw skali, który został właśnie utworzony przy użyciu informacji hello w [zarządzania maszynami wirtualnymi w zestawie skalowania maszyn wirtualnych](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="b2c27-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="b2c27-238">Więcej informacji o skalowaniu w pionie zawiera artykuł [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md) (Automatyczne skalowanie w pionie za pomocą zestawów skalowania maszyn wirtualnych)</span><span class="sxs-lookup"><span data-stu-id="b2c27-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="b2c27-239">Znajdź przykłady Azure Monitor funkcje w [Azure PowerShell Monitor szybki start — przykłady](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b2c27-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="b2c27-240">Dowiedz się więcej o funkcji powiadomień w [Użyj skalowania automatycznego akcje toosend poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="b2c27-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="b2c27-241">Dowiedz się, jak za[dzienniki inspekcji użycia w monitorze Azure, toosend poczty e-mail i elementu webhook powiadomień o alertach](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="b2c27-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

