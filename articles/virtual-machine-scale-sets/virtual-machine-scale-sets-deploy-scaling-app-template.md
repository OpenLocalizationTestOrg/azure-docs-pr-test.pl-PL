---
title: aaaDeploy aplikacji na podstawie zestawu skali maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się toodeploy proste Skalowanie automatyczne aplikacji w skali maszyny wirtualnej ustawić za pomocą szablonu usługi Azure Resource Manager."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="6354d-103">Wdrażanie aplikacji skalowania automatycznego przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="6354d-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="6354d-104">[Szablony usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) są toodeploy doskonały sposób grup powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6354d-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="6354d-105">W tym samouczku opiera się na [wdrożenia zestawu skali proste](virtual-machine-scale-sets-mvss-start.md) i w tym artykule opisano, jak toodeploy proste Skalowanie automatyczne aplikacji w skali ustawić za pomocą szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6354d-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="6354d-106">Można również skonfigurować przy użyciu programu PowerShell, interfejsu wiersza polecenia lub portalu hello Skalowanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="6354d-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="6354d-107">Aby uzyskać więcej informacji, zapoznaj się z [omówieniem skalowania automatycznego](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6354d-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="6354d-108">Dwa szablony szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="6354d-108">Two quickstart templates</span></span>
<span data-ttu-id="6354d-109">Podczas wdrażania zestawu skalowania można zainstalować nowe oprogramowanie na obrazie platformy przy użyciu [rozszerzenia maszyny wirtualnej](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="6354d-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="6354d-110">Rozszerzenie maszyny wirtualnej to mała aplikacja, która zapewnia konfigurację po wdrożeniu i zadania automatyzacji na maszynach wirtualnych Azure, takie jak wdrażanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6354d-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="6354d-111">Dwie przykładowe różne szablony znajdują się w [Azure/azure — Szybki Start — szablony](https://github.com/Azure/azure-quickstart-templates) wykazujących jak toodeploy aplikacji Skalowanie automatyczne na skali ustawić za pomocą rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6354d-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="6354d-112">Serwer HTTP Python w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6354d-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="6354d-113">Witaj [Python HTTP serwera w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) przykładowy szablon wdraża aplikację proste Skalowanie automatyczne, w systemie Linux zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="6354d-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="6354d-114">[Bottle](http://bottlepy.org/docs/dev/), Python sieci web framework i prosty serwer HTTP zostały wdrożone na każdej maszynie Wirtualnej w skali hello ustawić za pomocą skryptu niestandardowego rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6354d-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="6354d-115">Skala Hello skonfigurować skale gdy średnie wykorzystanie procesora CPU na wszystkich maszynach wirtualnych jest większa niż 60% i skalowany w dół, gdy hello średnie wykorzystanie procesora CPU jest mniej niż 30%.</span><span class="sxs-lookup"><span data-stu-id="6354d-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="6354d-116">Ponadto toohello zestawu skalowania zasobu hello *azuredeploy.json* przykładowy szablon deklaruje również sieć wirtualną, publiczny adres IP usługi równoważenia obciążenia i zasoby Ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="6354d-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="6354d-117">Aby uzyskać więcej informacji dotyczących tworzenia tych zasobów w szablonie, zobacz artykuł [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md) (Zestaw skalowania w systemie Linux obejmujący skalowanie automatyczne).</span><span class="sxs-lookup"><span data-stu-id="6354d-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="6354d-118">W hello *azuredeploy.json* szablonu, hello `extensionProfile` właściwości hello `Microsoft.Compute/virtualMachineScaleSets` zasobu określa rozszerzenie skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="6354d-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="6354d-119">`fileUris`Określa lokalizację, hello (ów).</span><span class="sxs-lookup"><span data-stu-id="6354d-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="6354d-120">W takim przypadku dwa pliki: *workserver.py*, który definiuje prosty serwer HTTP, i *installserver.sh*, co spowoduje zainstalowanie Bottle i uruchamia hello serwera HTTP.</span><span class="sxs-lookup"><span data-stu-id="6354d-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="6354d-121">`commandToExecute`Określa toorun polecenia powitania po wdrożeniu hello zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="6354d-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="6354d-122">Aplikacja platformy ASP.NET MVC w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="6354d-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="6354d-123">Witaj [aplikacji ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) przykładowy szablon wdraża prostej aplikacji ASP.NET MVC systemem zestaw skalowania systemu Windows w usługach IIS.</span><span class="sxs-lookup"><span data-stu-id="6354d-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="6354d-124">Usługi IIS i hello aplikacji MVC są wdrażane za pomocą hello [konfiguracji stanu (DSC) żądanego programu PowerShell](virtual-machine-scale-sets-dsc.md) rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6354d-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="6354d-125">Skala Hello skonfigurować skali (w wystąpieniu maszyny Wirtualnej w czasie) gdy wykorzystanie procesora CPU jest większa niż 50% 5 minut.</span><span class="sxs-lookup"><span data-stu-id="6354d-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="6354d-126">Ponadto toohello zestawu skalowania zasobu hello *azuredeploy.json* przykładowy szablon deklaruje również sieć wirtualną, publiczny adres IP usługi równoważenia obciążenia i zasoby Ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="6354d-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="6354d-127">Ten szablon przedstawia również uaktualnienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6354d-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="6354d-128">Aby uzyskać więcej informacji dotyczących tworzenia tych zasobów w szablonie, zobacz artykuł [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md) (Zestaw skalowania w systemie Windows obejmujący skalowanie automatyczne).</span><span class="sxs-lookup"><span data-stu-id="6354d-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="6354d-129">W hello *azuredeploy.json* szablonu, hello `extensionProfile` właściwości hello `Microsoft.Compute/virtualMachineScaleSets` zasobu określa [konfiguracji żądanego stanu (DSC)](virtual-machine-scale-sets-dsc.md) rozszerzenia, które instaluje usługi IIS i wartości domyślnej Aplikacja sieci Web z pakietu WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="6354d-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="6354d-130">Witaj *IISInstall.ps1* skrypt instaluje usługi IIS na maszynie wirtualnej hello i znajduje się w hello *DSC* folderu.</span><span class="sxs-lookup"><span data-stu-id="6354d-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="6354d-131">Aplikacja sieci web MVC Hello znajduje się w hello *WebDeploy* folderu.</span><span class="sxs-lookup"><span data-stu-id="6354d-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="6354d-132">skrypt instalacji toohello ścieżki Hello i aplikacji sieci web hello są zdefiniowane w hello `powershelldscZip` i `webDeployPackage` parametrów w hello *azuredeploy.parameters.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="6354d-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a><span data-ttu-id="6354d-133">Wdrażanie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="6354d-133">Deploy hello template</span></span>
<span data-ttu-id="6354d-134">Witaj najprostszy sposób toodeploy Witaj [Python HTTP serwera w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) lub [aplikacji ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) szablon jest toouse hello **wdrażanie tooAzure** znaleziono przycisku w hello w plikach readme hello w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6354d-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="6354d-135">Umożliwia także programu PowerShell lub interfejsu wiersza polecenia Azure toodeploy hello przykładowe szablony.</span><span class="sxs-lookup"><span data-stu-id="6354d-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="6354d-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6354d-136">PowerShell</span></span>
<span data-ttu-id="6354d-137">Kopiuj hello [Python HTTP serwera w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) lub [aplikacji ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) pliki z folderu tooa repozytorium GitHub hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6354d-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="6354d-138">Otwórz hello *azuredeploy.parameters.json* plików i aktualizacji hello wartościami domyślnymi hello `vmssName`, `adminUsername`, i `adminPassword` parametrów.</span><span class="sxs-lookup"><span data-stu-id="6354d-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="6354d-139">Zapisz hello następującego skryptu programu PowerShell za*deploy.ps1* hello — w tym samym folderze co hello *azuredeploy.json* szablonu.</span><span class="sxs-lookup"><span data-stu-id="6354d-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="6354d-140">toodeploy hello przykładowy szablon, uruchom hello *deploy.ps1* skryptu z okno poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6354d-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="6354d-141">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6354d-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a><span data-ttu-id="6354d-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6354d-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
