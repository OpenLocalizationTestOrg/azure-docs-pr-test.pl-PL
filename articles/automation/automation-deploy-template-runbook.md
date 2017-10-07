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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="54196-104">Wdrażanie szablonu usługi Azure Resource Manager w elemencie runbook programu PowerShell usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="54196-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="54196-105">Można napisać [runbook automatyzacji Azure w programie PowerShell](automation-first-runbook-textual-powershell.md) która wdraża zasobów platformy Azure przy użyciu [szablonu usługi Azure Resource Management](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="54196-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="54196-106">W ten sposób można zautomatyzować wdrożenie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="54196-107">Możesz zachować szablonów usługi Resource Manager w lokalizacji centralnej, bezpieczne, takie jak magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="54196-108">W tym temacie, utworzymy runbook programu PowerShell, która używa szablonu usługi Resource Manager przechowywane w [usługi Azure Storage](../storage/common/storage-introduction.md) toodeploy nowe konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54196-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="54196-109">Prerequisites</span></span>

<span data-ttu-id="54196-110">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="54196-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="54196-111">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-111">Azure subscription.</span></span> <span data-ttu-id="54196-112">Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="54196-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="54196-113">[Konto automatyzacji](automation-sec-configure-azure-runas-account.md) toohold hello elementu runbook i ich uwierzytelniać tooAzure zasobów.</span><span class="sxs-lookup"><span data-stu-id="54196-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="54196-114">To konto musi mieć uprawnienie toostart i zatrzymać hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54196-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="54196-115">[Konto usługi Azure Storage](../storage/common/storage-create-storage-account.md) w szablonie usługi Resource Manager hello które toostore</span><span class="sxs-lookup"><span data-stu-id="54196-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="54196-116">Program Azure Powershell jest zainstalowane na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="54196-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="54196-117">Zobacz [Instalowanie i konfigurowanie programu Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) informacje na temat tooget programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54196-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="54196-118">Tworzenie szablonu usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="54196-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="54196-119">W tym przykładzie używamy szablonu usługi Resource Manager, która wdraża nowe konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="54196-120">W edytorze tekstów skopiuj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="54196-120">In a text editor, copy hello following text:</span></span>

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

<span data-ttu-id="54196-121">Zapisz plik hello lokalnie jako `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="54196-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="54196-122">Zapisz hello szablonu usługi Resource Manager w usłudze Azure Storage</span><span class="sxs-lookup"><span data-stu-id="54196-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="54196-123">Po wprowadzeniu Użyj programu PowerShell toocreate udziału plików magazynu Azure i przekaż hello `TemplateTest.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="54196-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="54196-124">Aby uzyskać instrukcje dotyczące sposobu toocreate pliku udziału i przekazywanie pliku w hello portalu Azure, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="54196-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="54196-125">Na komputerze lokalnym, uruchom program PowerShell i uruchom hello następujące polecenia toocreate udziału plików i przekaż udziału plików toothat hello Menedżera zasobów szablonu.</span><span class="sxs-lookup"><span data-stu-id="54196-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

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

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="54196-126">Utwórz skrypt runbook PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="54196-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="54196-127">Teraz utworzymy skrypt programu PowerShell, który pobiera hello `TemplateTest.json` pliku z magazynu Azure i wdraża hello szablonu toocreate nowe konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="54196-128">W edytorze tekstów wklej hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="54196-128">In a text editor, paste hello following text:</span></span>

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

<span data-ttu-id="54196-129">Zapisz plik hello lokalnie jako `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="54196-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="54196-130">Importowanie i opublikować elementu runbook hello na koncie usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="54196-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="54196-131">Teraz możemy użyć programu PowerShell tooimport hello runbook do konta usługi Automatyzacja Azure, a następnie opublikuj hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="54196-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="54196-132">Aby uzyskać informacje na temat tooimport i opublikować element runbook w hello portalu Azure, zobacz [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="54196-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="54196-133">tooimport `DeployTemplate.ps1` na koncie automatyzacji jako elementu runbook programu PowerShell uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="54196-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

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

## <a name="start-hello-runbook"></a><span data-ttu-id="54196-134">Uruchom hello runbook</span><span class="sxs-lookup"><span data-stu-id="54196-134">Start hello runbook</span></span>

<span data-ttu-id="54196-135">Teraz Rozpoczniemy hello runbook przez wywołanie hello [Start AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="54196-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="54196-136">Aby uzyskać informacje o toostart elementu runbook w programie hello portalu Azure, zobacz temat [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="54196-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="54196-137">Uruchom następujące polecenia w konsoli programu PowerShell hello hello:</span><span class="sxs-lookup"><span data-stu-id="54196-137">Run hello following commands in hello PowerShell console:</span></span>

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

<span data-ttu-id="54196-138">Witaj działa element runbook, a jego stan można sprawdzić, uruchamiając `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="54196-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="54196-139">Hello runbook pobiera hello szablonu usługi Resource Manager i korzysta z niego toodeploy nowe konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="54196-140">Możesz sprawdzić, czy nowe konto magazynu hello została utworzona, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="54196-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="54196-141">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="54196-141">Summary</span></span>

<span data-ttu-id="54196-142">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="54196-142">That's it!</span></span> <span data-ttu-id="54196-143">Obecnie można użyć usługi Automatyzacja Azure i usługi Azure Storage i toodeploy szablony Menedżera zasobów wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="54196-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54196-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54196-144">Next steps</span></span>

* <span data-ttu-id="54196-145">toolearn więcej informacji na temat szablonów usługi Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="54196-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="54196-146">tooget pracy z magazynem Azure, zobacz [tooAzure wprowadzenie magazynu](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54196-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="54196-147">toofind inne przydatne elementy runbook automatyzacji Azure, zobacz [galerie elementów Runbook i modułów w automatyzacji Azure](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="54196-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="54196-148">toofind inne przydatne szablony Menedżera zasobów, zobacz [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="54196-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

