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
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="f0048-103">Utwórz maszynę Wirtualną za pomocą statycznego publicznego adresu IP za pomocą szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f0048-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0048-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f0048-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="f0048-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0048-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="f0048-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f0048-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="f0048-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="f0048-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="f0048-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="f0048-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f0048-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0048-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f0048-110">W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f0048-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="f0048-111">Zasoby adresów publicznych adresów IP w pliku szablonu</span><span class="sxs-lookup"><span data-stu-id="f0048-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="f0048-112">Można wyświetlić i pobrać hello [przykładowy szablon](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f0048-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="f0048-113">Witaj w tej części opisano hello definicji hello publicznego adresu IP zasobu na podstawie scenariusza hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="f0048-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

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

<span data-ttu-id="f0048-114">Powiadomienie hello **publicIPAllocationMethod** właściwość, która jest ustawiona zbyt*statycznych*.</span><span class="sxs-lookup"><span data-stu-id="f0048-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="f0048-115">Ta właściwość może być *dynamiczne* (wartość domyślna) lub *statycznych*.</span><span class="sxs-lookup"><span data-stu-id="f0048-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="f0048-116">Ustawienie gwarantuje toostatic, nigdy nie zmienia hello publiczny adres IP przypisany.</span><span class="sxs-lookup"><span data-stu-id="f0048-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="f0048-117">Witaj w tej części opisano hello skojarzenia hello publiczny adres IP z karty sieciowej:</span><span class="sxs-lookup"><span data-stu-id="f0048-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

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

<span data-ttu-id="f0048-118">Powiadomienie hello **publicznego adresu IP** Właściwość wskazująca toohello **identyfikator** zasobu o nazwie **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="f0048-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="f0048-119">To jest nazwa hello hello publicznego adresu IP zasobu przedstawionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="f0048-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="f0048-120">Na koniec interfejsu sieciowego hello powyżej ma na liście hello **networkProfile** właściwości hello Trwa tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0048-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="f0048-121">Wdrażanie szablonu hello przy użyciu kliknij toodeploy</span><span class="sxs-lookup"><span data-stu-id="f0048-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="f0048-122">Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej.</span><span class="sxs-lookup"><span data-stu-id="f0048-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="f0048-123">toodeploy przy użyciu tego szablonu kliknij toodeploy, kliknij przycisk **wdrażanie tooAzure** w pliku Readme.md hello hello [maszynę Wirtualną za pomocą statycznego adresu PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) szablonu.</span><span class="sxs-lookup"><span data-stu-id="f0048-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="f0048-124">Zastąp hello domyślne wartości parametrów w razie potrzeby, a następnie wprowadź wartości parametrów puste hello.</span><span class="sxs-lookup"><span data-stu-id="f0048-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="f0048-125">Wykonaj instrukcje hello hello portalu toocreate maszynę wirtualną za pomocą statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="f0048-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="f0048-126">Wdrażanie szablonu hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0048-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="f0048-127">toodeploy hello szablon, który został pobrany przy użyciu programu PowerShell, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="f0048-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="f0048-128">Jeśli nie znasz programu Azure PowerShell, pełną hello etapami hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f0048-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="f0048-129">W konsoli programu PowerShell, uruchom hello `New-AzureRmResourceGroup` toocreate polecenia cmdlet nową grupę zasobów, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="f0048-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="f0048-130">Jeśli masz już utworzoną grupę zasobów, przejdź toostep 3.</span><span class="sxs-lookup"><span data-stu-id="f0048-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="f0048-131">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f0048-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="f0048-132">W konsoli programu PowerShell, uruchom hello `New-AzureRmResourceGroupDeployment` szablonu hello toodeploy polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f0048-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="f0048-133">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f0048-133">Expected output:</span></span>
   
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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="f0048-134">Wdrażanie szablonu hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f0048-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="f0048-135">Szablon hello toodeploy przy użyciu hello Azure CLI, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f0048-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="f0048-136">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, wykonaj kroki hello w hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) artykuł tooinstall i skonfigurować go.</span><span class="sxs-lookup"><span data-stu-id="f0048-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="f0048-137">Uruchom hello `azure config mode` tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0048-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f0048-138">Witaj oczekiwane dane wyjściowe polecenia hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="f0048-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f0048-139">Otwórz hello [pliku parametrów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), zaznacz zawartością i zapisz go tooa plik na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="f0048-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="f0048-140">Na przykład parametry hello są zapisywane tooa plik o nazwie *parameters.JSON następującym kodem*.</span><span class="sxs-lookup"><span data-stu-id="f0048-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="f0048-141">Zmiany wartości parametrów hello w pliku hello w razie potrzeby, ale co najmniej, zaleca się zmianę wartości hello hello adminPassword parametru tooa unikatowy, złożone hasło.</span><span class="sxs-lookup"><span data-stu-id="f0048-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="f0048-142">Uruchom hello `azure group deployment create` cmd toodeploy hello nowej sieci wirtualnej przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego.</span><span class="sxs-lookup"><span data-stu-id="f0048-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f0048-143">W poleceniu hello poniżej, Zastąp <path> ze ścieżką hello został zapisany plik hello do.</span><span class="sxs-lookup"><span data-stu-id="f0048-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="f0048-144">Oczekiwane dane wyjściowe (znajduje się lista wartości parametrów używane):</span><span class="sxs-lookup"><span data-stu-id="f0048-144">Expected output (lists parameter values used):</span></span>

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

