---
title: "Wdrażanie aplikacji w zestawie skalowania maszyn wirtualnych platformy Azure | Microsoft Docs"
description: "Dowiedz się, jak wdrożyć prostą aplikację skalowania automatycznego w zestawie skalowania maszyn wirtualnych przy użyciu szablonu usługi Azure Resource Manager."
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
ms.openlocfilehash: 07883a33382cc660b043c99872312a9e77228253
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="b5cd4-103">Wdrażanie aplikacji skalowania automatycznego przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="b5cd4-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="b5cd4-104">[Szablony usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) to doskonały sposób wdrażania grup powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="b5cd4-105">Ten samouczek stanowi rozwinięcie tematu [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) (Wdrażanie prostego zestawu skalowania). Opisano w nim, jak wdrożyć prostą aplikację skalowania automatycznego w zestawie skalowania przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how to deploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="b5cd4-106">Skalowanie automatyczne można również skonfigurować przy użyciu programu PowerShell, interfejsu wiersza polecenia lub portalu.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-106">You can also set up autoscaling using PowerShell, CLI, or the portal.</span></span> <span data-ttu-id="b5cd4-107">Aby uzyskać więcej informacji, zapoznaj się z [omówieniem skalowania automatycznego](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5cd4-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="b5cd4-108">Dwa szablony szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="b5cd4-108">Two quickstart templates</span></span>
<span data-ttu-id="b5cd4-109">Podczas wdrażania zestawu skalowania można zainstalować nowe oprogramowanie na obrazie platformy przy użyciu [rozszerzenia maszyny wirtualnej](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="b5cd4-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="b5cd4-110">Rozszerzenie maszyny wirtualnej to mała aplikacja, która zapewnia konfigurację po wdrożeniu i zadania automatyzacji na maszynach wirtualnych Azure, takie jak wdrażanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="b5cd4-111">W folderze [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) znajdują się dwa różne przykładowe szablony, które przedstawiają, jak wdrożyć aplikację skalowania automatycznego do zestawu skalowania przy użyciu rozszerzeń maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how to deploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="b5cd4-112">Serwer HTTP Python w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="b5cd4-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="b5cd4-113">Przykładowy szablon [serwera HTTP Python w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) wdraża prostą aplikację skalowania automatycznego działającą w zestawie skalowania w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-113">The [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="b5cd4-114">[Bottle](http://bottlepy.org/docs/dev/), struktura sieci Web języka Python, oraz prosty serwer HTTP są wdrażane na każdej maszynie wirtualnej w zestawie skalowania przy użyciu rozszerzenia maszyny wirtualnej skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in the scale set using a custom script VM extension.</span></span> <span data-ttu-id="b5cd4-115">Zestaw skalowania jest skalowany w górę, gdy średnie wykorzystanie procesora na wszystkich maszynach wirtualnych przekracza 60%, lub w dół, gdy średnie wykorzystanie procesora jest mniejsze niż 30%.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-115">The scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when the average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="b5cd4-116">Oprócz zasobu zestawu skalowania przykładowy szablon *azuredeploy.json* deklaruje również sieć wirtualną, publiczny adres IP, moduł równoważenia obciążenia i zasoby ustawień skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-116">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="b5cd4-117">Aby uzyskać więcej informacji dotyczących tworzenia tych zasobów w szablonie, zobacz artykuł [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md) (Zestaw skalowania w systemie Linux obejmujący skalowanie automatyczne).</span><span class="sxs-lookup"><span data-stu-id="b5cd4-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="b5cd4-118">W szablonie *azuredeploy.json* właściwość `extensionProfile` zasobu `Microsoft.Compute/virtualMachineScaleSets` określa rozszerzenie skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-118">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="b5cd4-119">`fileUris` określa lokalizację skryptu.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-119">`fileUris` specifies the script(s) location.</span></span> <span data-ttu-id="b5cd4-120">W tym przypadku są to dwa pliki: *workserver.py*, który definiuje prosty serwer HTTP, i *installserver.sh*, który instaluje program Bottle i uruchamia serwer HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts the HTTP server.</span></span> <span data-ttu-id="b5cd4-121">`commandToExecute` określa polecenie do uruchomienia po wdrożeniu zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-121">`commandToExecute` specifies the command to run after the scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="b5cd4-122">Aplikacja platformy ASP.NET MVC w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="b5cd4-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="b5cd4-123">Przykładowy szablon [Aplikacja platformy ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) wdraża prostą aplikację platformy ASP.NET MVC działającą w środowisku IIS w zestawie skalowania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-123">The [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="b5cd4-124">Oprogramowanie IIS i aplikacja platformy MVC są wdrażane przy użyciu rozszerzenia maszyny wirtualnej [PowerShell Desired State Configuration (DSC)](virtual-machine-scale-sets-dsc.md).</span><span class="sxs-lookup"><span data-stu-id="b5cd4-124">IIS and the MVC app are deployed using the [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="b5cd4-125">Zestaw skalowania jest skalowany w górę (jednorazowo na jednym wystąpieniu maszyny wirtualnej), gdy wykorzystanie procesora przekracza 50% przez 5 minut.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-125">The scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="b5cd4-126">Oprócz zasobu zestawu skalowania przykładowy szablon *azuredeploy.json* deklaruje również sieć wirtualną, publiczny adres IP, moduł równoważenia obciążenia i zasoby ustawień skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-126">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="b5cd4-127">Ten szablon przedstawia również uaktualnienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="b5cd4-128">Aby uzyskać więcej informacji dotyczących tworzenia tych zasobów w szablonie, zobacz artykuł [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md) (Zestaw skalowania w systemie Windows obejmujący skalowanie automatyczne).</span><span class="sxs-lookup"><span data-stu-id="b5cd4-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="b5cd4-129">W szablonie *azuredeploy.json* właściwość `extensionProfile` zasobu `Microsoft.Compute/virtualMachineScaleSets` określa rozszerzenie [Desired State Configuration (DSC)](virtual-machine-scale-sets-dsc.md), które instaluje program IIS i domyślną aplikację sieci Web z pakietu WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-129">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="b5cd4-130">Skrypt *IISInstall.ps1* instaluje program IIS na maszynie wirtualnej i znajduje się w folderze *DSC*.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-130">The *IISInstall.ps1* script installs IIS on the virtual machine and is found in the *DSC* folder.</span></span>  <span data-ttu-id="b5cd4-131">Aplikacja sieci web MVC znajduje się w folderze *WebDeploy*.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-131">The MVC web app is found in the *WebDeploy* folder.</span></span>  <span data-ttu-id="b5cd4-132">Ścieżki do skryptu instalacji i aplikacji sieci Web są definiowane w parametrach `powershelldscZip` i `webDeployPackage` w pliku *azuredeploy.parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-132">The paths to the install script and the web app are defined in the `powershelldscZip` and `webDeployPackage` parameters in the *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="b5cd4-133">Wdrożenie szablonu</span><span class="sxs-lookup"><span data-stu-id="b5cd4-133">Deploy the template</span></span>
<span data-ttu-id="b5cd4-134">Najprostszym sposobem wdrażania szablonu [serwera HTTP Python w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) lub [aplikacji platformy ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) jest użycie przycisku **Wdróż na platformie Azure** znajdującego się w plikach Readme w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-134">The simplest way to deploy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is to use the **Deploy to Azure** button found in the in the readme files in GitHub.</span></span>  <span data-ttu-id="b5cd4-135">Aby wdrożyć przykładowe szablony, można również użyć programu PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-135">You can also use PowerShell or Azure CLI to deploy the sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="b5cd4-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5cd4-136">PowerShell</span></span>
<span data-ttu-id="b5cd4-137">Skopiuj pliki [serwera HTTP Python w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) lub [aplikacji platformy ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) z repozytorium serwisu GitHub do folderu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-137">Copy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from the GitHub repo to a folder on your local computer.</span></span>  <span data-ttu-id="b5cd4-138">Otwórz plik *azuredeploy.parameters.json* i zaktualizuj domyślne wartości parametrów `vmssName`, `adminUsername` i `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-138">Open the *azuredeploy.parameters.json* file and update the default values of the `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="b5cd4-139">Zapisz poniższy skrypt programu PowerShell do pliku *deploy.ps1* w tym samym folderze co szablon *azuredeploy.json*.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-139">Save the following PowerShell script to *deploy.ps1* in the same folder as the *azuredeploy.json* template.</span></span> <span data-ttu-id="b5cd4-140">Aby wdrożyć przykładowy szablon, uruchom skrypt *deploy.ps1* w oknie wiersza polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5cd4-140">To deploy the sample template run the *deploy.ps1* script from a PowerShell command window.</span></span>

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
    Write-Host "Resource group '$resourceGroupName' does not exist. To create a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start the deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="b5cd4-141">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b5cd4-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
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

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
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

## <a name="next-steps"></a><span data-ttu-id="b5cd4-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b5cd4-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
