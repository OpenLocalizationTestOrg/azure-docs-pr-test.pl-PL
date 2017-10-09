---
title: aaaAutoscale zestawy skalowania maszyny wirtualnej systemu Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="6c855-103">Automatycznie skalować maszyny z systemem Linux w zestawie skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="6c855-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="6c855-104">Zestawy skalowania maszyn wirtualnych ułatwiają możesz toodeploy i zarządzaj nimi wiele identycznych maszyn wirtualnych jako zestaw.</span><span class="sxs-lookup"><span data-stu-id="6c855-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="6c855-105">Zestawy skalowania w przypadku aplikacji o dużej skali zapewnić warstwy obliczeniowej wysoce skalowalnemu i dostosowania i obsługują obrazów platformy systemu Windows, Linux platformy obrazów niestandardowych obrazów i rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="6c855-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="6c855-106">toolearn więcej, zobacz [omówienie zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="6c855-107">Ten samouczek pokazuje, jak ustawić toocreate skalowania maszyn wirtualnych systemu Linux przy użyciu najnowszej wersji hello Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="6c855-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="6c855-108">Hello samouczek również pokazuje, jak ustawić tooautomatically skali hello maszyn w hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="6c855-109">Możesz utworzyć hello skalowalnego definiować skalowania przez utworzenie szablonu usługi Azure Resource Manager i wdrażanie za pomocą interfejsu wiersza polecenia Azure a.</span><span class="sxs-lookup"><span data-stu-id="6c855-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="6c855-110">Aby uzyskać więcej informacji na temat szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="6c855-111">toolearn więcej informacji na temat skalowania automatycznego zestawy skalowania, zobacz [automatyczne skalowanie i zestawach skali maszyny wirtualnej](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="6c855-112">W tym samouczku wdrożeniem hello następujących zasobów i rozszerzeń:</span><span class="sxs-lookup"><span data-stu-id="6c855-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="6c855-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="6c855-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="6c855-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="6c855-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="6c855-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="6c855-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="6c855-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="6c855-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="6c855-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="6c855-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="6c855-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="6c855-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="6c855-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="6c855-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="6c855-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="6c855-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="6c855-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="6c855-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="6c855-122">Aby uzyskać więcej informacji na temat zasoby usługi Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="6c855-123">Przed rozpoczęciem pracy z hello czynności w tym samouczku [zainstalować hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="6c855-124">Krok 1: Tworzenie grupy zasobów i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="6c855-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="6c855-125">**Zaloguj się tooMicrosoft Azure**</span><span class="sxs-lookup"><span data-stu-id="6c855-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="6c855-126">W interfejsie wiersza polecenia (Bash, terminali, wiersza polecenia), Przełącz tryb Manager tooResource, a następnie [Zaloguj się za pomocą identyfikatora firmy lub szkoły](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Wykonaj hello monity o tooyour środowisko logowania interakcyjnego konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c855-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="6c855-127">Jeśli masz służbowego lub szkolnego identyfikator i nie mają włączone uwierzytelnianie dwuskładnikowe, użyj `azure login -u` z toolog identyfikator hello w bez sesji interaktywnej.</span><span class="sxs-lookup"><span data-stu-id="6c855-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="6c855-128">Jeśli nie ma służbowego lub szkolnego identyfikator, możesz [Utwórz identyfikator firmy lub szkoły z osobistego konta Microsoft](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="6c855-129">**Utwórz grupę zasobów**</span><span class="sxs-lookup"><span data-stu-id="6c855-129">**Create a resource group**</span></span>  
<span data-ttu-id="6c855-130">Wszystkie zasoby musi być wdrożone tooa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c855-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="6c855-131">W tym samouczku, określ nazwę grupy zasobów hello **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="6c855-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="6c855-132">**Wdrażanie konta magazynu do nowej grupy zasobów hello**</span><span class="sxs-lookup"><span data-stu-id="6c855-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="6c855-133">To konto magazynu jest przechowywania hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="6c855-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="6c855-134">Utwórz konto magazynu o nazwie **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="6c855-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="6c855-135">Krok 2: Tworzenie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="6c855-135">Step 2: Create hello template</span></span>
<span data-ttu-id="6c855-136">Szablonu usługi Azure Resource Manager umożliwia możesz toodeploy i zarządzania zasobami Azure ze sobą przy użyciu opisu JSON zasobów hello i parametry skojarzonego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6c855-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="6c855-137">W edytorze Ulubione Utwórz plik hello VMSSTemplate.json i Dodaj hello początkowej JSON struktury toosupport hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="6c855-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="6c855-138">Parametry nie są zawsze wymagana, ale ich tooinput sposób wartości po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="6c855-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="6c855-139">Dodaj tych parametrów w obszarze hello elementu nadrzędnego dla parametrów czy dodany szablon toohello.</span><span class="sxs-lookup"><span data-stu-id="6c855-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="6c855-140">Nazwa dla hello oddzielne maszyny wirtualnej, która jest używana tooaccess hello maszyny w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="6c855-141">Nazwa dla konta magazynu hello przechowywania hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="6c855-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="6c855-142">Utwórz Hello liczbę wystąpień tooinitially maszyn wirtualnych w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="6c855-143">Nazwa i hasło konta administratora hello na maszynach wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="6c855-144">Ustaw prefiksu nazwy hello zasobów, które są tworzone toosupport hello skali.</span><span class="sxs-lookup"><span data-stu-id="6c855-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="6c855-145">Zmienne mogą być używane w wartości toospecify szablonów, które mogą ulec zmianie często lub wartości, które wymagają toobe utworzone na podstawie kombinację wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="6c855-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="6c855-146">Dodaj te zmienne w obszarze elementu nadrzędnego zmienne hello czy dodany szablon toohello.</span><span class="sxs-lookup"><span data-stu-id="6c855-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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

   * <span data-ttu-id="6c855-147">Nazwy DNS, które są używane przez hello interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="6c855-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="6c855-148">Witaj nazwy adresów IP i prefiksy hello sieci wirtualnej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="6c855-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="6c855-149">Witaj nazwy i identyfikatory hello sieci wirtualnej, obciążenia równoważenia i interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="6c855-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="6c855-150">Nazwy konta magazynu dla konta hello skojarzone z hello maszyny w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="6c855-151">Ustawienia dla hello diagnostyki rozszerzenia, które jest zainstalowane na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="6c855-152">Aby uzyskać więcej informacji na temat hello rozszerzenia diagnostyki, zobacz [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c855-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="6c855-153">Dodaj zasób konta magazynu hello pod elementem nadrzędnym zasobów hello czy dodany szablon toohello.</span><span class="sxs-lookup"><span data-stu-id="6c855-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="6c855-154">Ten szablon używa hello toocreate pętli, zalecane konta magazynu przechowywania hello dysków systemu operacyjnego i danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="6c855-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="6c855-155">Ten zestaw kont może obsługiwać zapasowych too100 maszyn wirtualnych w zestawie skalowania jest bieżąca maksymalna hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="6c855-156">Z określeniem literą, która została zdefiniowana w połączeniu z sufiks hello hello parametry podane dla szablonu hello zmiennych hello nosi nazwę każdego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6c855-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="6c855-157">Dodaj hello zasobów sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6c855-157">Add hello virtual network resource.</span></span> <span data-ttu-id="6c855-158">Aby uzyskać więcej informacji, zobacz [dostawcy zasobów sieciowych](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="6c855-159">Dodaj hello publicznego zasoby adresów IP używanych przez hello obciążenia równoważenia i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6c855-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="6c855-160">Dodaj zasób usługi równoważenia obciążenia hello, który jest używany przez zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="6c855-161">Aby uzyskać więcej informacji, zobacz [Obsługa Menedżera zasobów Azure dla usługi równoważenia obciążenia](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6c855-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="6c855-162">Dodaj hello sieci interfejsu zasób, który jest używany przez maszynę wirtualną z oddzielnych hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="6c855-163">Ponieważ maszyny w zestawie skalowania nie są dostępne za pośrednictwem publicznego adresu IP, oddzielnej maszynie wirtualnej jest tworzony w hello sam wirtualnych sieci tooremotely dostępu hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="6c855-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="6c855-164">Dodaj hello oddzielnej maszynie wirtualnej w hello sam sieci jako zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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

10. <span data-ttu-id="6c855-165">Dodaj zasób zestawu skalowania maszyny wirtualnej hello i określ hello diagnostyki rozszerzenia, które jest zainstalowany na wszystkich maszynach wirtualnych w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="6c855-166">Wiele ustawień powitania dla tego zasobu przypominają z hello zasobu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6c855-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="6c855-167">główne różnice Hello są hello pojemność elementu, który określa hello liczbę maszyn wirtualnych w zestawie skalowania hello i upgradePolicy określający, jak zaktualizowane toovirtual maszyny.</span><span class="sxs-lookup"><span data-stu-id="6c855-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="6c855-168">Witaj zestaw skalowania jest tworzone dopiero po wszystkich kont magazynu hello są tworzone z elementem dependsOn hello określonej.</span><span class="sxs-lookup"><span data-stu-id="6c855-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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

11. <span data-ttu-id="6c855-169">Dodaj zasób autoscaleSettings hello, który definiuje sposób oparte na wykorzystanie procesora na komputerach hello w zestawie hello dopasowuje zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
    
    <span data-ttu-id="6c855-170">W tym samouczku te wartości są ważne:</span><span class="sxs-lookup"><span data-stu-id="6c855-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="6c855-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="6c855-171">**metricName**</span></span>  
    <span data-ttu-id="6c855-172">Ta wartość jest hello taki sam jak hello licznika wydajności, zdefiniowanego w zmiennej wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="6c855-173">Za pomocą tej zmiennej, hello rozszerzenia diagnostycznych zbiera hello **Processor\PercentProcessorTime** licznika.</span><span class="sxs-lookup"><span data-stu-id="6c855-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="6c855-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="6c855-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="6c855-175">Ta wartość jest identyfikator zasobu hello zestaw skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="6c855-176">**ziarnem czasu**</span><span class="sxs-lookup"><span data-stu-id="6c855-176">**timeGrain**</span></span>  
    <span data-ttu-id="6c855-177">Ta wartość jest szczegółowości hello hello metryk, które są zbierane.</span><span class="sxs-lookup"><span data-stu-id="6c855-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="6c855-178">W tym szablonie ustawiono tooone minutę.</span><span class="sxs-lookup"><span data-stu-id="6c855-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="6c855-179">**Statystyka**</span><span class="sxs-lookup"><span data-stu-id="6c855-179">**statistic**</span></span>  
    <span data-ttu-id="6c855-180">Ta wartość określa, jak metryki hello są połączone tooaccommodate hello automatyczne skalowanie akcji.</span><span class="sxs-lookup"><span data-stu-id="6c855-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="6c855-181">Witaj możliwe wartości to: średnia, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="6c855-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="6c855-182">W tym szablonie są zbierane hello średni całkowite użycie Procesora hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6c855-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="6c855-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="6c855-183">**timeWindow**</span></span>  
    <span data-ttu-id="6c855-184">Ta wartość jest hello zakres czasu, w którym są zbierane dane wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="6c855-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="6c855-185">Musi być od 5 minut do 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="6c855-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="6c855-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="6c855-186">**timeAggregation**</span></span>  
    <span data-ttu-id="6c855-187">jego wartość określa, jak powinny być połączone hello dane, które są zbierane wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="6c855-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="6c855-188">Witaj domyślna wartość to średnia.</span><span class="sxs-lookup"><span data-stu-id="6c855-188">hello default value is Average.</span></span> <span data-ttu-id="6c855-189">Witaj możliwe wartości to: średnia, co najmniej, maksimum, ostatnich, łączna liczba, liczba.</span><span class="sxs-lookup"><span data-stu-id="6c855-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="6c855-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="6c855-190">**operator**</span></span>  
    <span data-ttu-id="6c855-191">Ta wartość jest hello operator, który jest używany toocompare hello metryki danych i hello próg.</span><span class="sxs-lookup"><span data-stu-id="6c855-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="6c855-192">Witaj możliwe wartości to: równa, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="6c855-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="6c855-193">**Próg**</span><span class="sxs-lookup"><span data-stu-id="6c855-193">**threshold**</span></span>  
    <span data-ttu-id="6c855-194">Ta wartość jest wyzwalane hello akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="6c855-194">This value triggers hello scale action.</span></span> <span data-ttu-id="6c855-195">W tym szablonie maszyn dodanych skali toohello ustawić, gdy hello średniego użycia procesora CPU między maszynami w zestawie hello jest ponad 50%.</span><span class="sxs-lookup"><span data-stu-id="6c855-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="6c855-196">**Kierunek**</span><span class="sxs-lookup"><span data-stu-id="6c855-196">**direction**</span></span>  
    <span data-ttu-id="6c855-197">Ta wartość określa akcji hello, wykonywaną, gdy uzyskuje się hello wartość progową.</span><span class="sxs-lookup"><span data-stu-id="6c855-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="6c855-198">Witaj możliwe wartości to zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="6c855-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="6c855-199">W tym szablonie hello liczbę maszyn wirtualnych w zestawie skalowania hello jest zwiększane, gdy próg hello jest ponad 50% hello określone okno czasu.</span><span class="sxs-lookup"><span data-stu-id="6c855-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="6c855-200">**Typ**</span><span class="sxs-lookup"><span data-stu-id="6c855-200">**type**</span></span>  
    <span data-ttu-id="6c855-201">Ta wartość jest typu hello akcji, która powinna się odbyć i musi być ustawione tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="6c855-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="6c855-202">**wartość**</span><span class="sxs-lookup"><span data-stu-id="6c855-202">**value**</span></span>  
    <span data-ttu-id="6c855-203">Ta wartość jest liczbą hello maszyn wirtualnych, które zostały dodane lub usunięte z hello zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="6c855-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="6c855-204">Ta wartość musi wynosić 1 lub większą.</span><span class="sxs-lookup"><span data-stu-id="6c855-204">This value must be 1 or greater.</span></span> <span data-ttu-id="6c855-205">Witaj, wartość domyślna to 1.</span><span class="sxs-lookup"><span data-stu-id="6c855-205">hello default value is 1.</span></span> <span data-ttu-id="6c855-206">W tym szablonie hello liczba maszyn w skali hello ustawić zwiększa 1, gdy zostały spełnione warunki progowe hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="6c855-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="6c855-207">**cooldown**</span></span>  
    <span data-ttu-id="6c855-208">Ta wartość jest hello ilość czasu toowait od momentu ostatniej akcji skalowania hello, zanim nastąpi hello następnej akcji.</span><span class="sxs-lookup"><span data-stu-id="6c855-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="6c855-209">Ta wartość musi należeć do zakresu od minutę i jeden tydzień.</span><span class="sxs-lookup"><span data-stu-id="6c855-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="6c855-210">Zapisz plik szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="6c855-211">Krok 3: Przekaż hello toostorage szablonu</span><span class="sxs-lookup"><span data-stu-id="6c855-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="6c855-212">można przekazać szablon Hello tak długo, jak znana nazwa hello i klucz podstawowy hello konta magazynu, który został utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="6c855-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="6c855-213">W interfejsie wiersza polecenia (Bash, terminali, wiersza polecenia) uruchom następujące polecenia, zmienne środowiskowe hello tooset potrzebne tooaccess hello konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="6c855-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="6c855-214">Klucz hello można uzyskać, klikając ikonę klucza hello podczas wyświetlania zasobów konta magazynu hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6c855-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="6c855-215">Korzystając z wiersza polecenia systemu Windows, wpisz **ustawić** zamiast eksportu.</span><span class="sxs-lookup"><span data-stu-id="6c855-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="6c855-216">Tworzenie kontenera hello do przechowywania szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="6c855-217">Przekaż hello szablon pliku toohello nowego kontenera.</span><span class="sxs-lookup"><span data-stu-id="6c855-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="6c855-218">Krok 4: Wdrażanie hello szablonu</span><span class="sxs-lookup"><span data-stu-id="6c855-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="6c855-219">Teraz, gdy utworzono szablon hello, możesz przystąpić do wdrażania hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c855-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="6c855-220">Użyj tego polecenia toostart hello procesu:</span><span class="sxs-lookup"><span data-stu-id="6c855-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="6c855-221">Po naciśnięciu wprowadź, zostanie wyświetlony monit o tooprovide wartości zmiennych hello, przypisana.</span><span class="sxs-lookup"><span data-stu-id="6c855-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="6c855-222">Podaj następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="6c855-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="6c855-223">Dla wszystkich toosuccessfully zasobów hello można wdrożyć powinien trwa około 15 minut.</span><span class="sxs-lookup"><span data-stu-id="6c855-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="6c855-224">Umożliwia także hello portal możliwości toodeploy hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c855-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="6c855-225">Użyj tego linku: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="6c855-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="6c855-226">Krok 5: Monitorowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="6c855-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="6c855-227">Można uzyskać informacji o zestawy skalowania maszyny wirtualnej za pomocą następujących metod:</span><span class="sxs-lookup"><span data-stu-id="6c855-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="6c855-228">Witaj Azure portal — można obecnie uzyskać ograniczoną ilość informacji za pomocą portalu hello.</span><span class="sxs-lookup"><span data-stu-id="6c855-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="6c855-229">Witaj [Eksploratora zasobów Azure](https://resources.azure.com/) — narzędzie to jest hello najlepsze do eksplorowania hello bieżącego stanu sieci zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="6c855-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="6c855-230">Tej ścieżki i powinna zostać wyświetlona zestawu widok wystąpienia hello skali hello utworzony:</span><span class="sxs-lookup"><span data-stu-id="6c855-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="6c855-231">Azure CLI — Użyj tego polecenia tooget niektóre informacje:</span><span class="sxs-lookup"><span data-stu-id="6c855-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="6c855-232">Łączenie maszyny wirtualnej jumpbox toohello, podobnie jak inne maszyny, a następnie można zdalnie przejść hello maszyn wirtualnych w hello skali zestaw toomonitor poszczególnych procesów.</span><span class="sxs-lookup"><span data-stu-id="6c855-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="6c855-233">Zakończenie interfejsu API REST do uzyskiwania informacji na temat zestawów skalowania można znaleźć w [zestawach skali maszyny wirtualnej](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c855-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="6c855-234">Krok 6: Usuń zasoby hello</span><span class="sxs-lookup"><span data-stu-id="6c855-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="6c855-235">Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="6c855-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="6c855-236">Nie trzeba toodelete każdego zasobu niezależnie od grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c855-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="6c855-237">Można usunąć grupy zasobów hello i wszystkie jej zasoby są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="6c855-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="6c855-238">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c855-238">Next steps</span></span>
* <span data-ttu-id="6c855-239">Znajdź przykłady Azure Monitor funkcje w [Azure Monitor i platform interfejsu wiersza polecenia Szybki start — przykłady](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="6c855-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="6c855-240">Dowiedz się więcej o funkcji powiadomień w [Użyj skalowania automatycznego akcje toosend poczty e-mail i elementu webhook powiadomień o alertach w monitorze Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="6c855-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="6c855-241">Dowiedz się, jak za[dzienniki inspekcji użycia w monitorze Azure, toosend poczty e-mail i elementu webhook powiadomień o alertach](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="6c855-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="6c855-242">Zapoznaj się z hello [aplikacja demonstracyjna skalowania automatycznego na Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) szablonu, który konfiguruje hello tooexercise aplikacji Python/bottle automatyczne skalowanie funkcji zestawach skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6c855-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

