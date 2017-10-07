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
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="f0a0d-103">Tworzenie sieci za pomocą szablonu usługi Azure Resource Manager grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="f0a0d-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f0a0d-104">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="f0a0d-105">Możesz również [tworzenia grup NSG w hello klasycznego modelu wdrażania](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0d-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="f0a0d-106">Grupa NSG zasobów w pliku szablonu</span><span class="sxs-lookup"><span data-stu-id="f0a0d-106">NSG resources in a template file</span></span>
<span data-ttu-id="f0a0d-107">Można wyświetlić i pobrać hello [przykładowy szablon](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="f0a0d-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="f0a0d-108">Witaj w tej części opisano hello definicji hello frontonu NSG, oparte na powitania scenariusza.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

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
<span data-ttu-id="f0a0d-109">tooassociate hello NSG toohello frontonu podsieci, masz toochange hello podsieci definicji szablonu hello i identyfikator odwołania hello Użyj hello NSG.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

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

<span data-ttu-id="f0a0d-110">Zwróć uwagę, hello wykonywana w ramach hello zaplecza NSG hello zaplecza podsieci i w szablonie hello takie same.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="f0a0d-111">Wdrażanie szablonu ARM hello przy użyciu kliknij toodeploy</span><span class="sxs-lookup"><span data-stu-id="f0a0d-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="f0a0d-112">Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="f0a0d-113">toodeploy przy użyciu tego szablonu kliknij toodeploy, postępuj zgodnie z [to łącze](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów w razie potrzeby i wykonaj te instrukcje hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="f0a0d-114">Wdrażanie szablonu ARM hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0a0d-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="f0a0d-115">Szablon ARM hello toodeploy, który został pobrany przy użyciu programu PowerShell, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="f0a0d-116">Jeśli nie znasz programu Azure PowerShell, postępuj zgodnie z instrukcjami hello hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall i skonfigurować go.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="f0a0d-117">Uruchom hello  **`New-AzureRmResourceGroup`**  toocreate polecenia cmdlet, grupy zasobów przy użyciu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="f0a0d-118">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f0a0d-118">Expected output:</span></span>

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

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="f0a0d-119">Wdrażanie szablonu ARM hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f0a0d-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="f0a0d-120">Szablon ARM hello toodeploy przy użyciu hello wiersza polecenia platformy Azure, wykonaj kroki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="f0a0d-121">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f0a0d-122">Uruchom hello  **`azure config mode`**  tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f0a0d-123">Oto Hello hello oczekiwane dane wyjściowe polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="f0a0d-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f0a0d-124">Uruchom hello  **`azure group deployment create`**  hello toodeploy polecenia cmdlet nowej sieci wirtualnej przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f0a0d-125">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="f0a0d-126">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f0a0d-126">Expected output:</span></span>
   
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
   
   * <span data-ttu-id="f0a0d-127">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-127">**-n (or --name)**.</span></span> <span data-ttu-id="f0a0d-128">Nazwa toobe grupy zasobów hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="f0a0d-129">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-129">**-l (or --location)**.</span></span> <span data-ttu-id="f0a0d-130">Region platformy Azure, w której zostanie utworzona hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="f0a0d-131">**-f (lub --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="f0a0d-132">Ścieżka pliku szablonu ARM tooyour.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="f0a0d-133">**-e (lub --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="f0a0d-134">Ścieżka pliku parametrów ARM tooyour.</span><span class="sxs-lookup"><span data-stu-id="f0a0d-134">Path tooyour ARM parameters file.</span></span>

