---
title: "aaaDeploy szablonu usługi Azure Resource Manager w element runbook usługi Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "Jak toodeploy szablonu usługi Azure Resource Manager przechowywane w usłudze Azure Storage z poziomu elementu runbook"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "środowiska PowerShell, elementu runbook, json, usługi Automatyzacja azure"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Wdrażanie szablonu usługi Azure Resource Manager w elemencie runbook programu PowerShell usługi Automatyzacja Azure

Można napisać [runbook automatyzacji Azure w programie PowerShell](automation-first-runbook-textual-powershell.md) która wdraża zasobów platformy Azure przy użyciu [szablonu usługi Azure Resource Management](../azure-resource-manager/resource-manager-create-first-template.md).

W ten sposób można zautomatyzować wdrożenie zasobów platformy Azure. Możesz zachować szablonów usługi Resource Manager w lokalizacji centralnej, bezpieczne, takie jak magazyn Azure.

W tym temacie, utworzymy runbook programu PowerShell, która używa szablonu usługi Resource Manager przechowywane w [usługi Azure Storage](../storage/common/storage-introduction.md) toodeploy nowe konto magazynu Azure.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka należy hello następujące:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).
* [Konto automatyzacji](automation-sec-configure-azure-runas-account.md) toohold hello elementu runbook i ich uwierzytelniać tooAzure zasobów.  To konto musi mieć uprawnienie toostart i zatrzymać hello maszyny wirtualnej.
* [Konto usługi Azure Storage](../storage/common/storage-create-storage-account.md) w szablonie usługi Resource Manager hello które toostore
* Program Azure Powershell jest zainstalowane na komputerze lokalnym. Zobacz [Instalowanie i konfigurowanie programu Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) informacje na temat tooget programu Azure PowerShell.

## <a name="create-hello-resource-manager-template"></a>Tworzenie szablonu usługi Resource Manager hello

W tym przykładzie używamy szablonu usługi Resource Manager, która wdraża nowe konto magazynu Azure.

W edytorze tekstów skopiuj hello następującego tekstu:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

Zapisz plik hello lokalnie jako `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Zapisz hello szablonu usługi Resource Manager w usłudze Azure Storage

Po wprowadzeniu Użyj programu PowerShell toocreate udziału plików magazynu Azure i przekaż hello `TemplateTest.json` pliku.
Aby uzyskać instrukcje dotyczące sposobu toocreate pliku udziału i przekazywanie pliku w hello portalu Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../storage/files/storage-dotnet-how-to-use-files.md).

Na komputerze lokalnym, uruchom program PowerShell i uruchom hello następujące polecenia toocreate udziału plików i przekaż udziału plików toothat hello Menedżera zasobów szablonu.

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a>Utwórz skrypt runbook PowerShell hello

Teraz utworzymy skrypt programu PowerShell, który pobiera hello `TemplateTest.json` pliku z magazynu Azure i wdraża hello szablonu toocreate nowe konto magazynu Azure.

W edytorze tekstów wklej hello następującego tekstu:

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

Zapisz plik hello lokalnie jako `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>Importowanie i opublikować elementu runbook hello na koncie usługi Automatyzacja Azure

Teraz możemy użyć programu PowerShell tooimport hello runbook do konta usługi Automatyzacja Azure, a następnie opublikuj hello elementu runbook.
Aby uzyskać informacje na temat tooimport i opublikować element runbook w hello portalu Azure, zobacz [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` na koncie automatyzacji jako elementu runbook programu PowerShell uruchom następujące polecenia programu PowerShell hello:

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a>Uruchom hello runbook

Teraz Rozpoczniemy hello runbook przez wywołanie hello [Start AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) polecenia cmdlet.

Aby uzyskać informacje o toostart elementu runbook w programie hello portalu Azure, zobacz temat [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md).

Uruchom następujące polecenia w konsoli programu PowerShell hello hello:

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

Witaj działa element runbook, a jego stan można sprawdzić, uruchamiając `$job.Status`.

Hello runbook pobiera hello szablonu usługi Resource Manager i korzysta z niego toodeploy nowe konto magazynu Azure.
Możesz sprawdzić, czy nowe konto magazynu hello została utworzona, uruchamiając następujące polecenie hello:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Podsumowanie

Gotowe. Obecnie można użyć usługi Automatyzacja Azure i usługi Azure Storage i toodeploy szablony Menedżera zasobów wszystkich zasobów na platformie Azure.

## <a name="next-steps"></a>Następne kroki

* toolearn więcej informacji na temat szablonów usługi Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* tooget pracy z magazynem Azure, zobacz [tooAzure wprowadzenie magazynu](../storage/common/storage-introduction.md).
* toofind inne przydatne elementy runbook automatyzacji Azure, zobacz [galerie elementów Runbook i modułów w automatyzacji Azure](automation-runbook-gallery.md).
* toofind inne przydatne szablony Menedżera zasobów, zobacz [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/)

