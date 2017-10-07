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
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Wdrażanie aplikacji skalowania automatycznego przy użyciu szablonu

[Szablony usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) są toodeploy doskonały sposób grup powiązanych zasobów. W tym samouczku opiera się na [wdrożenia zestawu skali proste](virtual-machine-scale-sets-mvss-start.md) i w tym artykule opisano, jak toodeploy proste Skalowanie automatyczne aplikacji w skali ustawić za pomocą szablonu usługi Azure Resource Manager.  Można również skonfigurować przy użyciu programu PowerShell, interfejsu wiersza polecenia lub portalu hello Skalowanie automatyczne. Aby uzyskać więcej informacji, zapoznaj się z [omówieniem skalowania automatycznego](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>Dwa szablony szybkiego startu
Podczas wdrażania zestawu skalowania można zainstalować nowe oprogramowanie na obrazie platformy przy użyciu [rozszerzenia maszyny wirtualnej](../virtual-machines/virtual-machines-windows-extensions-features.md). Rozszerzenie maszyny wirtualnej to mała aplikacja, która zapewnia konfigurację po wdrożeniu i zadania automatyzacji na maszynach wirtualnych Azure, takie jak wdrażanie aplikacji. Dwie przykładowe różne szablony znajdują się w [Azure/azure — Szybki Start — szablony](https://github.com/Azure/azure-quickstart-templates) wykazujących jak toodeploy aplikacji Skalowanie automatyczne na skali ustawić za pomocą rozszerzeń maszyny Wirtualnej.

### <a name="python-http-server-on-linux"></a>Serwer HTTP Python w systemie Linux
Witaj [Python HTTP serwera w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) przykładowy szablon wdraża aplikację proste Skalowanie automatyczne, w systemie Linux zestaw skali.  [Bottle](http://bottlepy.org/docs/dev/), Python sieci web framework i prosty serwer HTTP zostały wdrożone na każdej maszynie Wirtualnej w skali hello ustawić za pomocą skryptu niestandardowego rozszerzenia maszyny Wirtualnej. Skala Hello skonfigurować skale gdy średnie wykorzystanie procesora CPU na wszystkich maszynach wirtualnych jest większa niż 60% i skalowany w dół, gdy hello średnie wykorzystanie procesora CPU jest mniej niż 30%.

Ponadto toohello zestawu skalowania zasobu hello *azuredeploy.json* przykładowy szablon deklaruje również sieć wirtualną, publiczny adres IP usługi równoważenia obciążenia i zasoby Ustawienia skalowania automatycznego.  Aby uzyskać więcej informacji dotyczących tworzenia tych zasobów w szablonie, zobacz artykuł [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md) (Zestaw skalowania w systemie Linux obejmujący skalowanie automatyczne).

W hello *azuredeploy.json* szablonu, hello `extensionProfile` właściwości hello `Microsoft.Compute/virtualMachineScaleSets` zasobu określa rozszerzenie skryptu niestandardowego. `fileUris`Określa lokalizację, hello (ów). W takim przypadku dwa pliki: *workserver.py*, który definiuje prosty serwer HTTP, i *installserver.sh*, co spowoduje zainstalowanie Bottle i uruchamia hello serwera HTTP. `commandToExecute`Określa toorun polecenia powitania po wdrożeniu hello zestaw skali.

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

### <a name="aspnet-mvc-application-on-windows"></a>Aplikacja platformy ASP.NET MVC w systemie Windows
Witaj [aplikacji ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) przykładowy szablon wdraża prostej aplikacji ASP.NET MVC systemem zestaw skalowania systemu Windows w usługach IIS.  Usługi IIS i hello aplikacji MVC są wdrażane za pomocą hello [konfiguracji stanu (DSC) żądanego programu PowerShell](virtual-machine-scale-sets-dsc.md) rozszerzenia maszyny Wirtualnej.  Skala Hello skonfigurować skali (w wystąpieniu maszyny Wirtualnej w czasie) gdy wykorzystanie procesora CPU jest większa niż 50% 5 minut. 

Ponadto toohello zestawu skalowania zasobu hello *azuredeploy.json* przykładowy szablon deklaruje również sieć wirtualną, publiczny adres IP usługi równoważenia obciążenia i zasoby Ustawienia skalowania automatycznego. Ten szablon przedstawia również uaktualnienie aplikacji.  Aby uzyskać więcej informacji dotyczących tworzenia tych zasobów w szablonie, zobacz artykuł [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md) (Zestaw skalowania w systemie Windows obejmujący skalowanie automatyczne).

W hello *azuredeploy.json* szablonu, hello `extensionProfile` właściwości hello `Microsoft.Compute/virtualMachineScaleSets` zasobu określa [konfiguracji żądanego stanu (DSC)](virtual-machine-scale-sets-dsc.md) rozszerzenia, które instaluje usługi IIS i wartości domyślnej Aplikacja sieci Web z pakietu WebDeploy.  Witaj *IISInstall.ps1* skrypt instaluje usługi IIS na maszynie wirtualnej hello i znajduje się w hello *DSC* folderu.  Aplikacja sieci web MVC Hello znajduje się w hello *WebDeploy* folderu.  skrypt instalacji toohello ścieżki Hello i aplikacji sieci web hello są zdefiniowane w hello `powershelldscZip` i `webDeployPackage` parametrów w hello *azuredeploy.parameters.json* pliku. 

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

## <a name="deploy-hello-template"></a>Wdrażanie szablonu hello
Witaj najprostszy sposób toodeploy Witaj [Python HTTP serwera w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) lub [aplikacji ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) szablon jest toouse hello **wdrażanie tooAzure** znaleziono przycisku w hello w plikach readme hello w serwisie GitHub.  Umożliwia także programu PowerShell lub interfejsu wiersza polecenia Azure toodeploy hello przykładowe szablony.

### <a name="powershell"></a>PowerShell
Kopiuj hello [Python HTTP serwera w systemie Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) lub [aplikacji ASP.NET MVC w systemie Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) pliki z folderu tooa repozytorium GitHub hello na komputerze lokalnym.  Otwórz hello *azuredeploy.parameters.json* plików i aktualizacji hello wartościami domyślnymi hello `vmssName`, `adminUsername`, i `adminPassword` parametrów. Zapisz hello następującego skryptu programu PowerShell za*deploy.ps1* hello — w tym samym folderze co hello *azuredeploy.json* szablonu. toodeploy hello przykładowy szablon, uruchom hello *deploy.ps1* skryptu z okno poleceń programu PowerShell.

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

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
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

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
